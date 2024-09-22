Returns the pet type or a 404 error.

```toml
name = 'Get a pet type by ID'
description = '/pettypes/{petTypeId}'
method = 'GET'
url = '{{baseUrl}}/pettypes/{petTypeId}'
sortWeight = 3000000
id = 'd1086cc1-02b7-4088-aa27-38b399a9fabd'

[[pathVariables]]
key = 'petTypeId'
description = 'The ID of the pet type.'
```
