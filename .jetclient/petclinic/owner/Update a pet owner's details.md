Updates the pet owner record with the specified details.

```toml
name = "Update a pet owner's details"
description = '/owners/{ownerId}'
method = 'PUT'
url = '{{baseUrl}}/owners/{ownerId}'
sortWeight = 4000000
id = '4914215d-8376-42af-89f0-8b8bd36021d8'

[[pathVariables]]
key = 'ownerId'
description = 'The ID of the pet owner.'

[body]
type = 'JSON'
raw = '''
{
  "firstName": "",
  "lastName": "",
  "address": "",
  "city": "",
  "telephone": ""
}'''
```
