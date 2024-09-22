Returns the pet type or a 404 error.

```toml
name = 'Update a pet type by ID'
description = '/pettypes/{petTypeId}'
method = 'PUT'
url = '{{baseUrl}}/pettypes/{petTypeId}'
sortWeight = 4000000
id = '29465323-d58e-4826-ae40-d54753eb8d77'

[[pathVariables]]
key = 'petTypeId'
description = 'The ID of the pet type.'

[body]
type = 'JSON'
raw = '''
{
  "name": "",
  "id": 0
}'''
```
