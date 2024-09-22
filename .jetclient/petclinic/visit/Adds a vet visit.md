Records the details of a new vet visit.

```toml
name = 'Adds a vet visit'
description = '/owners/{ownerId}/pets/{petId}/visits'
method = 'POST'
url = '{{baseUrl}}/owners/{ownerId}/pets/{petId}/visits'
sortWeight = 1000000
id = '9738e225-a697-419a-a8a3-f95a4fd8b53e'

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
  "date": "2024-09-22",
  "description": ""
}'''
```
