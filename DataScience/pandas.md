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

## Links

How to use pandas effectively [https://github.com/TomAugspurger/effective-pandas]