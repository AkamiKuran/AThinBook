# HTTP API

## Common HTTP Methods

| Method Name | Usage         |
| ----------- | ------------- |
| GET         | Retrieve resource |
|POST| Create a new resource|
| PUT| Replace a resource|
|PATCH|Update a resource|
|DELETE|Delete a resource|

get response
```python
res = requests.get(URL)
res.text
res.json()
res.status_code
```

| Status Codes | Meaning               |
| ------------ | --------------------- |
| 200          | OK                    |
| 201          | Created               |
| 400          | Bad Request           |
| 403          | Forbidden             |
| 404          | Not Found             |
| 405          | Method not allowed    |
| 422          | Un-processable Entity |

# HTML5 HTTP history

- pushState
- onpopstate

# HTML5 Window

![image-20201003224711372](pic\image-20201003224445774.png)