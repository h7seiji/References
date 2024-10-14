# Pandas

## Tips

### inplace=True should not be used when modifying a Pandas DataFrame

Use method chaining instead

```python
result = df.drop('City', axis=1).sort_values('Name').reset_index(drop=True)
```

### More complex loc

```python
df['C'] = df['A'].apply(lambda x: my_dict.get(x))

filtered_df = df.loc[df['C'] == value]
```
