





# interact with HTML

## return HTML

```python
@app.route('/')
def index():
    return "<h1>hello!</h1>"
```



## render HTML file

```python
from flask import render_template
@app.route('/')
def index():
    return render_template('index.html')
```





# Pass Parameters

## Flask to Flask

``` python
@app.route("/<string:name>")
def hello(name):
	pass
```



## Flask to Template

### Pass Variables

```python
def index():
    headline = 'hello'
    return render_template('index.html', headline=headline)
```

```html
<!DOCTYPE html>
<html>
    <head>
        <h1>
            {{headline}}
        </h1>
    </head>    
</html>
```
Support [Jinja](https://jinja.palletsprojects.com/en/2.11.x/)

```html
<!--pass variable: new_year-->
<!DOCTYPE html>
<html>
    <body>
        {% if new_year %}
        <h1>Yes!</h1>
        {% else %}
        <h1>No!</h1>
        {% end if %}
    </body>    
</html>
```

```html
<a href="{{ url_for('more')}}">see more</a>
<!--Indicates to visit the flask-defined url "/more"-->
```





### Pass Blocks

## HTML TO HTML

