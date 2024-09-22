Creates a vet .

```toml
name = 'Create a Vet'
description = '/vets'
method = 'POST'
url = '{{baseUrl}}/vets'
sortWeight = 2000000
id = 'd617f1a4-b209-4c7a-a0b6-87180e144e78'

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
