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

### Example

Creates Owner Admin

```toml
name = 'Owner Admin'
id = '336bd1b7-307d-4c5d-9ad0-863b66e665b2'

[body]
type = 'JSON'
raw = '''
{
  "username": "{{ownerAdminUsername}}",
  "password": "{{ownerAdminPassword}}",
  "enabled": true,
  "roles": [
    {
      "name": "ROLE_OWNER_ADMIN"
    }
  ]
}'''
```

### Example

Creates Vet Admin

```toml
name = 'Vet Admin'
id = '3599a8f6-5262-44d5-b8c9-059ebffd7dc1'

[body]
type = 'JSON'
raw = '''
{
  "username": "{{vetAdminUsername}}",
  "password": "{{vetAdminPassword}}",
  "enabled": true,
  "roles": [
    {
      "name": "ROLE_VET_ADMIN"
    }
  ]
}'''
```
