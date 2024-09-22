```toml
name = 'Delete pets'
sortWeight = 2000000
id = '1808eec3-7b16-442d-8c81-28c47c9d8fd0'
```

#### Script

```js
const listPetsResponse = await jc.sendRequestAsync("Lists pet")
const petIds = listPetsResponse.code === 404 ? [] : listPetsResponse.json("$[*].id")

for (let petId of petIds) {
    const response = await jc.sendRequestAsync('Delete a pet by ID', req =>
        req.setPathVariables({petId})
    )
    jc.expect(response.code).to.be.oneOf([204, 404])
}

```
