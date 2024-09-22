Records the details of a new pet.

```toml
name = 'Adds a pet to an owner'
description = '/owners/{ownerId}/pets'
method = 'POST'
url = '{{baseUrl}}/owners/{ownerId}/pets'
sortWeight = 1000000
id = '4d7bcb79-adb3-40dd-a951-9d7a0577b810'

[[pathVariables]]
key = 'ownerId'
description = 'The ID of the pet owner.'

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
