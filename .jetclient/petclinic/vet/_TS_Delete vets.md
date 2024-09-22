```toml
name = 'Delete vets'
sortWeight = 2000000
id = '619a9b36-2cd9-4687-a760-5ee36c078278'
```

#### Script

```js
const listVetsResponse = jc.sendRequest("Lists vets")
const vetIds = listVetsResponse.code === 404 ? [] : listVetsResponse.json("$[*].id")

for (let vetId of vetIds) {
    jc.sendRequestAsync('Delete a vet by ID', r => r.setPathVariables({vetId}))
        .then(response => {
            response.to.have.status(204)
        })
}
```
