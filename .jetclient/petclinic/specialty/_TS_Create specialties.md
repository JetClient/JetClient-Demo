```toml
name = 'Create specialties'
sortWeight = 1000000
id = '3c4cc510-9e96-4a8c-9670-af67ada4fad8'
```

#### Variables

```json5
{
  specialties: [
    {
      name: "radiology",
    },
    {
      name: "surgery",
    },
    {
      name: "dentistry",
    }
  ]
}
```

#### Script

```js
const specialtyPromises = jc.variables.get("specialties").map(specialty =>
    jc.sendRequestAsync("Create a specialty", withJsonBody(specialty))
        .then(response => {
            response.to.have.status(201)
            const responseBody = response.json()
            jc.expect(responseBody).to.have.property("id")

            const specialtyWithoutId = _.omit(responseBody, 'id')

            jc.expect(specialtyWithoutId).to.deep.equal(specialty)
            return responseBody
        })
)

return await Promise.all(specialtyPromises)

```
