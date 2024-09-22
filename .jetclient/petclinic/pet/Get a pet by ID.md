Returns the pet or a 404 error.

```toml
name = 'Get a pet by ID'
description = '/owners/{ownerId}/pets/{petId}'
method = 'GET'
url = '{{baseUrl}}/owners/{ownerId}/pets/{petId}'
sortWeight = 2000000
id = '1576fa33-bd9d-41c1-81c3-51b4de4c96be'

[[pathVariables]]
key = 'ownerId'
description = 'The ID of the pet owner.'

[[pathVariables]]
key = 'petId'
description = 'The ID of the pet.'
```
