Returns the specialty or a 404 error.

```toml
name = 'Update a specialty by ID'
description = '/specialties/{specialtyId}'
method = 'PUT'
url = '{{baseUrl}}/specialties/{specialtyId}'
sortWeight = 4000000
id = 'a486fd93-d4cb-4fd4-b21c-63ccf774048a'

[[pathVariables]]
key = 'specialtyId'
description = 'The ID of the specialty.'

[body]
type = 'JSON'
raw = '''
{
  "id": 0,
  "name": ""
}'''
```
