```toml
name = 'Delete owners'
sortWeight = 2000000
id = '2939b4d9-ca7e-4b0b-9032-4ed25701f276'
```

#### Script

```js
const listOwnersResponse = await jc.sendRequestAsync("Lists pet owners")
const ownerIds = listOwnersResponse.code === 404 ? [] : listOwnersResponse.json("$[*].id")

for (let ownerId of ownerIds) {
    jc.sendRequestAsync('Delete an owner by ID', req =>
        req.setPathVariables({ownerId})
    ).then(response => {
        response.to.have.status(204)
    })
}
```
