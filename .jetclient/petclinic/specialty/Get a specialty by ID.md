Returns the specialty or a 404 error.

```toml
name = 'Get a specialty by ID'
description = '/specialties/{specialtyId}'
method = 'GET'
url = '{{baseUrl}}/specialties/{specialtyId}'
sortWeight = 3000000
id = '46159c16-b5fe-4fae-a3a4-7327bfd87f2e'

[[pathVariables]]
key = 'specialtyId'
description = 'The ID of the speciality.'
```
