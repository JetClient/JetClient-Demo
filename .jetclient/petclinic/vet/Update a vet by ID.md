Returns the vet or a 404 error.

```toml
name = 'Update a vet by ID'
description = '/vets/{vetId}'
method = 'PUT'
url = '{{baseUrl}}/vets/{vetId}'
sortWeight = 4000000
id = '573c36da-736a-431e-89fc-2363ab2b5ef1'

[[pathVariables]]
key = 'vetId'
description = 'The ID of the vet.'

[body]
type = 'JSON'
raw = '''
{
  "firstName": "",
  "lastName": "",
  "specialties": [
    {
      "id": 0,
      "name": ""
    }
  ],
  "id": 0
}'''
```
