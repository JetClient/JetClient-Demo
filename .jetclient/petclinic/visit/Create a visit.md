Creates a visit.

```toml
name = 'Create a visit'
description = '/visits'
method = 'POST'
url = '{{baseUrl}}/visits'
sortWeight = 3000000
id = '23facfbb-3d0a-43fd-9074-9b2c9160d114'

[body]
type = 'JSON'
raw = '''
{
  "date": "2024-09-22",
  "description": "",
  "id": 0,
  "petId": 0
}'''
```
