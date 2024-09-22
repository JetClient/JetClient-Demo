Returns the pet type or a 404 error.

```toml
name = 'Delete a pet type by ID'
description = '/pettypes/{petTypeId}'
method = 'DELETE'
url = '{{baseUrl}}/pettypes/{petTypeId}'
sortWeight = 5000000
id = 'defc2ff2-ddf1-457a-aa76-b2bcc99046b5'

[[pathVariables]]
key = 'petTypeId'
description = 'The ID of the pet type.'
```
