```toml
name = 'Pet Clinic'
id = 'fed954cc-4b7a-413c-b51e-e464776e4491'

[[environmentGroups]]
name = 'Default'
environments = ['Local']

[[environmentGroups]]
name = 'User'
environments = ['Admin', 'Owner Admin', 'Vet Admin']

[[apis]]
name = 'API'
[apis.openApi]
file = 'openapi.yml'
```

#### Variables

```json5
{
  local: {
    baseUrl: 'http://localhost:9966/petclinic/api'
  },
  admin: {
    // Typically, credentials are stored in Local variables
    // to avoid sharing them in the source code.
    // For the purpose of this demo, we're keeping them in Shared variables.
    username: 'admin',
    password: 'admin',
  },
  owner_admin: {
    username: 'ownerAdmin',
    password: 'ownerAdminPassword'
  },
  vet_admin: {
    username: 'vetAdmin',
    password: 'vetAdminPassword'
  }
}
```

#### Init Script

```js
withJsonBody = function (body) {
    return request => request.setBodyJson(body)
}
```
