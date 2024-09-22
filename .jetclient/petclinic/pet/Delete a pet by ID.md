Returns the pet or a 404 error.

```toml
name = 'Delete a pet by ID'
description = '/pets/{petId}'
method = 'DELETE'
url = '{{baseUrl}}/pets/{petId}'
sortWeight = 7000000
id = '4acd5495-d314-4a22-89c8-5c5d379ca788'

[[pathVariables]]
key = 'petId'
description = 'The ID of the pet.'
```
