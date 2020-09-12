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

trend_bar|trend_line
```

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

## Múltiple
```python
hist_brain = alt.Chart(brain).mark_bar().encode(
    x=alt.X('Brain Weight', bin=alt.Bin(maxbins=50)),
    y= 'count()'
).interactive()

hist_body = alt.Chart(brain).mark_bar().encode(
    x=alt.X('Body Weight', bin=alt.Bin(maxbins=50)),
    y= 'count()'
).interactive()

scatter_brain_body = alt.Chart(brain).mark_circle().encode(
    x=alt.X('Body Weight', bin=alt.Bin(maxbins=50)),
    y= 'Brain Weight'
).interactive()

(hist_brain|hist_body)&scatter_brain_body

```

scatter_brain_body = alt.Chart(brain).mark_circle().encode(
    x=alt.X('Body Weight', bin=alt.Bin(maxbins=50)),
    y= 'Brain Weight'
).interactive()


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
## Create themes

```python
# Incluir temas a los gráficos
# Primero crear un archivo de configuración
config = {'arc': {'fill': '#30a2da'}, 
'area': {'fill': 'black'}, 
'axisBand': {'grid': False}, 
'axisBottom': {'domain': False, 
'domainColor': '#999', 
'domainWidth': 3, 
'grid': False, 
'gridColor': '#cbcbcb', 
'gridWidth': 1, 
'labelColor': '#999', 
'labelFontSize': 14, 
'labelPadding': 4, 
'tickColor': 'white', 
'tickSize': 10, 
'titleFontSize': 14, 
'titlePadding': 10}, 
'axisLeft': {'domainColor': 'white', 
'domainWidth': 1, 
'grid': False, 
'gridColor': 'white', 
'gridWidth': 1, 
'labelColor': 'white', 
'labelFontSize': 10, 
'labelPadding': 4, 
'tickColor': 'white', 
'tickSize': 10, 
'ticks': True, 
'titleFontSize': 14, 
'titlePadding': 10}, 
'axisRight': {'domainColor': '#333',
'domainWidth': 1, 
'grid': True, 
'gridColor': '#cbcbcb', 
'gridWidth': 1, 
'labelColor': 'white', 
'labelFontSize': 10, 
'labelPadding': 4, 
'tickColor': 'white', 
'tickSize': 10, 
'ticks': True, 
'titleFontSize': 14, 
'titlePadding': 10}, 
'axisTop': {'domain': False, 
'domainColor': '#333', 
'domainWidth': 3, 
'grid': False, 
'gridColor': '#cbcbcb', 
'gridWidth': 1, 
'labelColor': '#999', 
'labelFontSize': 10, 
'labelPadding': 4, 
'tickColor': '#cbcbcb', 
'tickSize': 10, 
'titleFontSize': 14, 
'titlePadding': 10}, 
'background': 'white', 
'group': {'fill': 'black',"stroke":"white"}, 
'legend': {'labelColor': '#333', 
'labelFontSize': 14, 
'padding': 1, 
'symbolSize': 30, 
'symbolType': 'square', 
'titleColor': '#333', 
'titleFontSize': 14, 
'titlePadding': 10}, 
'line': {'stroke': '#30a2da', 'strokeWidth': 2}, 
'path': {'stroke': '#30a2da', 'strokeWidth': 0.5}, 
'rect': {'fill': '#30a2da'}, 
'range': {'category': ['#30a2da', 
'#fc4f30', 
'#e5ae38', 
'#6d904f', 
'#8b8b8b', 
'#b96db8', 
'#ff9e27', 
'#56cc60', 
'#52d2ca', 
'#52689e', 
'#545454', 
'#9fe4f8'], 
'diverging': ['#cc0020', 
'#e77866', 
'#f6e7e1', 
'#d6e8ed', 
'#91bfd9', 
'#1d78b5'], 
'heatmap': ['#d6e8ed', '#cee0e5', '#91bfd9', '#549cc6', '#1d78b5']}, 
'symbol': {'filled': True, 'shape': 'circle'}, 
'shape': {'stroke': 'white'}, 
'style': {'bar': {'binSpacing': 2, 'fill': '#30a2da', 'stroke': None}}, 
'title': {'anchor': 'start', 'fontSize': 24, 'fontWeight': 600, 'offset': 20},
"view": { 
"stroke": "transparent" 
}}

# Y luego lo registro
def my_theme(): 
  return {'config': config } 

alt.themes.register('my_theme', my_theme) 

alt.themes.enable('my_theme')
```
