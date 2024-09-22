Creates a user.

```toml
name = 'Create a user'
description = '/users'
method = 'POST'
url = '{{baseUrl}}/users'
sortWeight = 1000000
id = '5599e932-c404-4fc9-9d8f-543dd2bd49bb'

[body]
type = 'JSON'
raw = '''
{
  "username": "",
  "password": "",
  "enabled": false,
  "roles": [
    {
      "name": ""
    }
  ]
}'''
```
