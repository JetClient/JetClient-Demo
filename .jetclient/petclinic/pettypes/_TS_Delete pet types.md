```toml
name = 'Delete pet types'
sortWeight = 2000000
id = '15334202-eb4e-4171-aee2-a3df7ca45d82'
```

#### Script

```js
const listPetTypesResponse = jc.sendRequest("Lists pet types")
const petTypeIds = listPetTypesResponse.code === 404 ? [] : listPetTypesResponse.json("$[*].id")

for (let petTypeId of petTypeIds) {
    jc.sendRequestAsync('Delete a pet type by ID', r => r.setPathVariables({petTypeId}))
        .then(response => {
            response.to.have.status(204)
        })
}
```
