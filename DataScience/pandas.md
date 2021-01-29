# Pandas

## Snippets

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
## Links

How to use pandas effectively [https://github.com/TomAugspurger/effective-pandas]