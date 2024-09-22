Creates a specialty .

```toml
name = 'Create a specialty'
description = '/specialties'
method = 'POST'
url = '{{baseUrl}}/specialties'
sortWeight = 2000000
id = '6ee8a6e6-ccf2-4a76-8558-c704129e53f6'

[body]
type = 'JSON'
raw = '''
{
  "id": 0,
  "name": ""
}'''
```
