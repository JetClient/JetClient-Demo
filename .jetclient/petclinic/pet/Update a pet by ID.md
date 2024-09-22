Returns the pet or a 404 error.

```toml
name = 'Update a pet by ID'
description = '/pets/{petId}'
method = 'PUT'
url = '{{baseUrl}}/pets/{petId}'
sortWeight = 6000000
id = 'f3185697-7b49-4c93-aceb-a01a108a9c19'

[[pathVariables]]
key = 'petId'
description = 'The ID of the pet.'

[body]
type = 'JSON'
raw = '''
{
  "name": "",
  "birthDate": "2024-09-22",
  "type": {
    "name": "",
    "id": 0
  },
  "id": 0,
  "ownerId": 0,
  "visits": [
    {
      "date": "2024-09-22",
      "description": "",
      "id": 0,
      "petId": 0
    }
  ]
}'''
```
