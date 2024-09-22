Returns the pet  or a 404 error.

```toml
name = 'Get a pet by ID'
description = '/pets/{petId}'
method = 'GET'
url = '{{baseUrl}}/pets/{petId}'
sortWeight = 5000000
id = '1953dfd5-b8eb-4a58-a3e6-ec1786b71c4c'

[[pathVariables]]
key = 'petId'
description = 'The ID of the pet.'
```
