# Overview

## Using % and .format()

'{} {}'.format('one', 'two')
print("Hello {}, your balance is {}.".format("Adam", 230.2346))
print("Hello {name}, your balance is {blc}.".format(name="Adam", blc=230.2346))

More useful and info: https://pyformat.info

## Cambiar color celda Jupyter Notebook

```python
from IPython.display import HTML, display
def set_background(color):    
    script = (
        "var cell = this.closest('.jp-CodeCell');"
        "var editor = cell.querySelector('.jp-Editor');"
        "editor.style.background='{}';"
        "this.parentNode.removeChild(this)"
    ).format(color)

display(HTML('<img src onerror="{}">'.format(script)))

set_background('honeydew')
```
