Records the details of a new pet owner.

```toml
name = 'Adds a pet owner'
description = '/owners'
method = 'POST'
url = '{{baseUrl}}/owners'
sortWeight = 2000000
id = '550bf505-5eca-4ea6-b1bb-95a9c2528065'

[body]
type = 'JSON'
raw = '''
{
  "firstName": "",
  "lastName": "",
  "address": "",
  "city": "",
  "telephone": ""
}'''
```
