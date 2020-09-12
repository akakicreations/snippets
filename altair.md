# Overview

## Bar Chart

```python

hist_brain = alt.Chart(brain).mark_bar().encode(
    x=alt.X('Brain Weight', bin=alt.Bin(maxbins=50)),
    y= 'count()'
).interactive()
```

```python

## Scatter Bar

alt.Chart(brain).mark_circle().encode(
    x=alt.X('Body Weight', bin=alt.Bin(maxbins=50)),
    y= 'Brain Weight'
).properties(
    width=600,
    height=300,
    title="RElacióón peso del cerebro y del cuerpo"
)
```
