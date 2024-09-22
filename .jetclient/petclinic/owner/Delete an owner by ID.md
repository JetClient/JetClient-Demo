Returns the owner or a 404 error.

```toml
name = 'Delete an owner by ID'
description = '/owners/{ownerId}'
method = 'DELETE'
url = '{{baseUrl}}/owners/{ownerId}'
sortWeight = 5000000
id = 'b0aea353-a7db-4220-bcd5-fe713faef055'

[[pathVariables]]
key = 'ownerId'
description = 'The ID of the owner.'
```
