# Snippets

## Pandas

### show table as markdown inside notebook

```python
def pandas_df_to_markdown_table(df):
    from IPython.display import Markdown, display
    fmt = ['---'] * df.shape[1]
    df_fmt = pd.DataFrame([fmt], columns=df.columns)
    df_formatted = pd.concat([df_fmt, df])
    display(Markdown(df_formatted.to_csv(sep="|", index=False)))

pandas_df_to_markdown_table(target_customer)
```

### sample DataFrame equally from each class

```python
nrows = len(df)
total_sample_size = 1e4
df.groupby('classes').\
    apply(lambda x: x.sample(int(x.count()/nrows)*total_sample_size)))
```
from [https://stackoverflow.com/questions/40645524/how-can-i-sample-equally-from-a-dataframe]

## Plotting

### folium: map with time slider: compare two points moving on map

```python
def compare_traces(trace1, trace2):
    coords1 = [[i.LONGITUDE, i.LATITUDE] for i in trace1.itertuples()]
    time1 = [str(i.TIME) for i in trace1.itertuples()]
    coords2 = [[i.LONGITUDE, i.LATITUDE] for i in trace2.itertuples()]
    time2 = [str(i.TIME) for i in trace2.itertuples()]

    m = folium.Map(
        location=[trace1.LATITUDE.mean(), trace1.LONGITUDE.mean()],
        zoom_start=7,
        tiles="cartodbpositron",
        width=900,
        height=900
    )

    plugins.TimestampedGeoJson({
        'type': 'FeatureCollection',
        'features': [
          {
            'type': 'Feature',
            'geometry': {
              'type': 'LineString',
              'coordinates':coords1,
              },
            'properties': {
              'times': time1,
              'style': {
                  'color': 'blue',
                  'opacity': 0.5
              },
              "icon": "circle",
              "iconstyle": {
                  "fillColor": "blue",
                  "fillOpacity": 0.6,
                  "radius": 2,
              },
              }
            },
            {
            'type': 'Feature',
            'geometry': {
              'type': 'LineString',
              'coordinates':coords2,
              },
            'properties': {
              'times': time2,
              'style': {
                  'color': 'red',
                  'opacity': 0.5
              },
              "icon": "circle",
              "iconstyle": {
                "fillColor": "red",
                "fillOpacity": 0.6,
                "radius": 2,
              },
              }
            }
          ]
        },
        period="PT30S",
        duration='PT15M',
        add_last_point=True,
    ).add_to(m)

    return m
```

### matplotlib: error bands

```python
import matplotlib.pyplot as plt

plt.figure( figsize=(20, 20) )

fig = df.plot(x = 'DATE', y = ['MEAN', 'UPPER_BAND', 'LOWER_BAND'])
fig.fill_between(x = df['DATE'], y1 = df['LOWER_BAND'], y2 = df['UPPER_BAND'], alpha = 0.2, color = 'green')
```

## Links

How to use pandas effectively [https://github.com/TomAugspurger/effective-pandas]