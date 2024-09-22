Returns the vet or a 404 error.

```toml
name = 'Delete a vet by ID'
description = '/vets/{vetId}'
method = 'DELETE'
url = '{{baseUrl}}/vets/{vetId}'
sortWeight = 5000000
id = 'a6f67a18-84ed-43ce-a8dc-21ae5fbb07a3'

[[pathVariables]]
key = 'vetId'
description = 'The ID of the vet.'
```
