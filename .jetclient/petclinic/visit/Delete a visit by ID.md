Returns the visit or a 404 error.

```toml
name = 'Delete a visit by ID'
description = '/visits/{visitId}'
method = 'DELETE'
url = '{{baseUrl}}/visits/{visitId}'
sortWeight = 6000000
id = '59705507-806c-40b9-aedf-b903e1d99b8d'

[[pathVariables]]
key = 'visitId'
description = 'The ID of the visit.'
```
