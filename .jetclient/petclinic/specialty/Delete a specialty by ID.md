Returns the specialty or a 404 error.

```toml
name = 'Delete a specialty by ID'
description = '/specialties/{specialtyId}'
method = 'DELETE'
url = '{{baseUrl}}/specialties/{specialtyId}'
sortWeight = 5000000
id = 'bc2db186-a7e1-4052-8b2f-3de102e4c5fd'

[[pathVariables]]
key = 'specialtyId'
description = 'The ID of the specialty.'
```
