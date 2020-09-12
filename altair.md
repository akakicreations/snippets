# Overview

## Bar Chart

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

```
