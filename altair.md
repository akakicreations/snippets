# Overview

## Line Bar

```python
alt.Chart(trends).mark_line().encode(
    x= 'yearmonth(date):T',
    y="mean(value)",
    color='search_term'
).properties(  
title="Titleeeee" 
).interactive() 

```

## Bar Chart
```python

alt.Chart(brain).mark_bar().encode(
    x=alt.X('Brain Weight', bin=alt.Bin(maxbins=50)),
    y= 'count()'
).interactive()
```

## Scatter Bar
```python
alt.Chart(brain).mark_circle().encode(
    x=alt.X('Body Weight', bin=alt.Bin(maxbins=50)),
    y= 'Brain Weight'
).properties(
    width=600,
    height=300,
    title="RElacióón peso del cerebro y del cuerpo"
)
```

