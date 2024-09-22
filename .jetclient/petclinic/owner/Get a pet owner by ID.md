Returns the pet owner or a 404 error.

```toml
name = 'Get a pet owner by ID'
description = '/owners/{ownerId}'
method = 'GET'
url = '{{baseUrl}}/owners/{ownerId}'
sortWeight = 3000000
id = '5895290f-8f3b-4acd-bda4-2352e4654763'

[[pathVariables]]
key = 'ownerId'
description = 'The ID of the pet owner.'
```
