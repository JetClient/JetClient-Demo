Updates the pet record with the specified details.

```toml
name = "Update a pet's details"
description = '/owners/{ownerId}/pets/{petId}'
method = 'PUT'
url = '{{baseUrl}}/owners/{ownerId}/pets/{petId}'
sortWeight = 3000000
id = '4012ccc6-f0be-4df6-a1c2-48418f362ec1'

[[pathVariables]]
key = 'ownerId'
description = 'The ID of the pet owner.'

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
  }
}'''
```
