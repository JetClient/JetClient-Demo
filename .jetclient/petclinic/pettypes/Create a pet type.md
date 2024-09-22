Creates a pet type .

```toml
name = 'Create a pet type'
description = '/pettypes'
method = 'POST'
url = '{{baseUrl}}/pettypes'
sortWeight = 2000000
id = '9b691145-f009-4232-9d00-e41dc3a7458f'

[body]
type = 'JSON'
raw = '''
{
  "name": ""
}'''
```
