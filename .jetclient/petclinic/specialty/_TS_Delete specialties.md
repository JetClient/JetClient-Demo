```toml
name = 'Delete specialties'
sortWeight = 2000000
id = '353f4a87-ff8a-4cc4-bbab-6826bb73281d'
```

#### Script

```js
const listSpecialtiesResponse = jc.sendRequest("Lists specialties")
const specialtyIds = listSpecialtiesResponse.code === 404 ? [] : listSpecialtiesResponse.json("$[*].id")

for (let specialtyId of specialtyIds) {
    jc.sendRequestAsync('Delete a specialty by ID', r => r.setPathVariables({specialtyId}))
        .then(response => {
            response.to.have.status(204)
        })
}
```
