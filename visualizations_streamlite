# Overview

## CELDAS QUE REPRODUCIR

```python
# (Para local + Colab)
# Instalar Streamlite
!pip install streamlit -q
```

```python
# (Para Colab)
!wget https://bin.equinox.io/c/4VmDzA7iaHb/ngrok-stable-linux-amd64.zip
!unzip -qq ngrok-stable-linux-amd64.zip
```

```python
# (Para Colab)
# Nos da la URL donde se verá el streamlit
get_ipython().system_raw('./ngrok http 8501 &')
! curl -s http://localhost:4040/api/tunnels | python3 -c \
"import sys, json; print(json.load(sys.stdin)['tunnels'][0]['public_url'])"
```

```python
# (Para local + Colab)
%%file hello.py

# Esto está dentro del archivo hello.py
import streamlit as st 
import pandas as pd
import altair as alt 
import matplotlib.pyplot as plt 

st.title("Hello world") 

# Mostrar tablas de datos 
brain = pd.read_csv("https://raw.githubusercontent.com/rezpe/datos_viz/master/brain.csv") 
st.table(brain.head()) 

# Mostrar texto 
st.markdown(" Texto de ejepmplo") 

# Altair 
hist_brain = alt.Chart(brain).mark_bar().encode( 
x=alt.X('Brain Weight',bin=alt.Bin(maxbins=100)), 
y="count()" 
).properties( 
width=300, 
height=150, 
title="Relación peso del cerebro y del cuerpo" 
).interactive() 

hist_body = alt.Chart(brain).mark_bar().encode( 
x=alt.X('Body Weight',bin=alt.Bin(maxbins=100)), 
y="count()" 
).properties( 
width=300, 
height=150, 
title="Relación peso del cerebro y del cuerpo" 
).interactive() 

scatter_brain_body = alt.Chart(brain).mark_circle().encode( 
x='Body Weight', 
y='Brain Weight' 
).properties( 
width=700, 
height=300, 
title="Relación peso del cerebro y del cuerpo" 
).interactive() 

comp_brain = (hist_brain|hist_body)&scatter_brain_body 
st.write(comp_brain)
```
```python
# (Para local + Colab)
# Así hacemos que se pueda acceder a la web
# Se queda ejecutando continuamente
!streamlit run hello.py
```
## Prueba completa en collab
```python
# Inicio
get_ipython().system_raw('./ngrok http 8501 &')
! curl -s http://localhost:4040/api/tunnels | python3 -c \
"import sys, json; print(json.load(sys.stdin)['tunnels'][0]['public_url'])"
```

```python
# Inicio
# Código
%%file hello.py
import streamlit as st 
import pandas as pd
import altair as alt 

st.title("GDP Life expectancy") 

# Mostrar texto 
st.markdown("No gathered xxxx xxxxx xxxx") 

# Mostrar grafico 
lifecountries = pd.read_csv("https://raw.githubusercontent.com/rezpe/datos_viz/master/lifecountries.csv")

scatter_expectancy = alt.Chart(lifecountries).mark_circle().encode( 
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

st.write(scatter_expectancy)
```

```python
# Ejecutar
!streamlit run hello.py
```

## Ejemplo con interactividad

```python
# Inicio
get_ipython().system_raw('./ngrok http 8501 &')
! curl -s http://localhost:4040/api/tunnels | python3 -c \
"import sys, json; print(json.load(sys.stdin)['tunnels'][0]['public_url'])"
```

```python
# Código
%%file hello.py
import streamlit as st 
import pandas as pd
import altair as alt 

st.title("GDP Life expectancy") 

texto = st.text_input('Insert value')

st.markdown(f"El texto que has escrito es: " + texto)
```

```python
# Ejecutar
!streamlit run hello.py
```

