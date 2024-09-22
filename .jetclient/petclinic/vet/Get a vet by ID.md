Returns the vet or a 404 error.

```toml
name = 'Get a vet by ID'
description = '/vets/{vetId}'
method = 'GET'
url = '{{baseUrl}}/vets/{vetId}'
sortWeight = 3000000
id = '015a2ce8-231a-4a82-a5ab-baf48ee6828d'

[[pathVariables]]
key = 'vetId'
description = 'The ID of the vet.'
```
