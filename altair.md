# Overview

## Line Bar

```python
alt.Chart(trends).mark_line().encode(
    x= 'yearmonth(date):T',
    y="mean(value)",
    color='search_term'
).properties(  
title="Title" 
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
    title="Title"
)
```

## Scatter + Line
```python
trend_line = alt.Chart(trends).mark_line().encode(
    x= 'yearmonth(date):T',
    y="mean(value)",
    color='search_term'
).properties(  
title="Titleeeee" 
).interactive() 

trend_bar = alt.Chart(trends).mark_bar().encode( 
x="search_term", 
y="value", 
color="search_term" 
).properties(  
title="Titleeeee" 
).interactive()
```
trend_bar|trend_line

## Bar + Line with filter
```python
select_term = alt.selection(type='single', encodings=['x'])

trend_line = alt.Chart(trends).mark_line().encode(
    x= 'yearmonth(date):T',
    y="mean(value)",
    color='search_term'
).properties(  
title="Titleeeee" 
).transform_filter(
    select_term
)


trend_bar = alt.Chart(trends).mark_bar().encode( 
x="search_term", 
y="value", 
color="search_term", 
tooltip='search_term'
).properties(  
title="Titleeeee",
selection=select_term 
)

trend_bar|trend_line
```

## Bar + Line with filter, one up, one down
```python
select_date = alt.selection(type='interval', encodings=['x'])

trend_line = alt.Chart(trends).mark_line().encode(
    x= 'yearmonth(date):T',
    y="mean(value)",
    color='search_term'
).properties( 
width=700,
height=100,
title="XXXXXX",  
selection=select_date 
)

mini_trend_line = alt.Chart(trends).mark_line().encode(
    x= 'yearmonth(date):T',
    y="mean(value)",
    color='search_term'
).properties( 
width=700, 
height=300,
title="XXXXXX",  
selection=select_date 
).transform_filter(
    select_date
)

trend_line&mini_trend_line
```

## Complex Scatter
```python
scatter_brain_body = alt.Chart(lifecountries).mark_circle().encode( 
    x='Life Expectancy', 
    y='Country GDP', 
    color='Continent', 
    size='size',
    tooltip='Continent'
).properties( 
    width=700, 
    height=300, 
    title="Scatter plot" 
).interactive() 

scatter_brain_body
```

## Map
```python
# Ir a http://geojson.io/#map=2/20.0/0.0 donde se podría construir el mapa
# O buscar un mapa ya construido en formato geojson, ejemplo: https://github.com/datasets/geo-countries

##### ESTO SON LOS PUNTOS
temp = world_temp.groupby("city").mean().reset_index()
points = alt.Chart(temp).mark_circle().encode(
    latitude="lat", 
    longitude="lon",
    tooltip="city",
    color= alt.Color('mean(temp)', scale=alt.Scale(domain=[-20,10,40], range=['lightblue', 'orange', 'red']))
).properties(
        width= 1000,
        height= 700,
    )

##### ESTO VA A SER EL FONDO
# remote geojson data object
url = "https://raw.githubusercontent.com/datasets/geo-countries/master/data/countries.geojson" 
data_geojson_remote = alt.Data(url=url, format=alt.DataFormat(property='features',type='json')) 

# chart object 
background = alt.Chart(data_geojson_remote).mark_geoshape(
    fill='lightgrey',
    stroke = 'white'
).encode( 
color="properties.name:N" 
).properties( 
    width= 1000,
    height= 700,
projection={'type': 'identity', 'reflectY': True} 
)

background+points
```
