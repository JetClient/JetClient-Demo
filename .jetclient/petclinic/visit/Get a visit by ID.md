Returns the visit or a 404 error.

```toml
name = 'Get a visit by ID'
description = '/visits/{visitId}'
method = 'GET'
url = '{{baseUrl}}/visits/{visitId}'
sortWeight = 4000000
id = 'a729a0ea-93c2-41cc-ab94-21ccb6acb4ba'

[[pathVariables]]
key = 'visitId'
description = 'The ID of the visit.'
```
