```toml
name = 'User Tests'
sortWeight = 1000000
id = 'bf932e36-7d34-4602-9abd-2a1c0d6b6cb5'
```

#### Variables

```json5
{
  ownerAdminUser: {
    username: 'ownerAdmin',
    password: 'ownerAdminPassword',
    enabled: true,
    roles: [
      {
        "name": "ROLE_OWNER_ADMIN"
      }
    ]
  },
  badUser: {
    password: "password",
    enabled: true,
    roles: [
      {
        "name": "ROLE_OWNER_ADMIN"
      }
    ]
  }
}
```

#### Script

```js
jc.testCase("Create user success", () => {
    const user = jc.variables.get("ownerAdminUser")

    const response = jc.sendRequest("Create a user", withJsonBody(user))
    response.to.have.status(201)
    response.to.have.jsonBody(user)
})

jc.testCase("Create user error", () => {
    const badUser = jc.variables.get("badUser")

    const response = jc.sendRequest("Create a user", withJsonBody(badUser))
    response.to.have.status(400)
})

```
