Returns the visit or a 404 error.

```toml
name = 'Update a visit by ID'
description = '/visits/{visitId}'
method = 'PUT'
url = '{{baseUrl}}/visits/{visitId}'
sortWeight = 5000000
id = '61fd3b7c-ab6b-4076-aabd-03bef4c33ca3'

[[pathVariables]]
key = 'visitId'
description = 'The ID of the visit.'

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
