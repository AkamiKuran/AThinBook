# Variable Section

Top layout: layout.html

```html
<h1>
	{% block heading %}
    {% endblock %}
</h1>
<body>
    {% block body %}
    {% endblock %}
</body>
```

Detailed layout

```html
{% extends "layout.html" %}
{% block body %}
	<p>
        Writing sth.
	</p>
{% endblock %}
```

