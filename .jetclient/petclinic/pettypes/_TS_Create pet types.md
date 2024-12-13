```toml
name = 'Create pet types'
sortWeight = 1000000
id = 'de04852f-448a-4490-89e9-4e70f92a862b'
```

#### Variables

```json5
{
  allPetTypes: [
    {
      name: "cat",
    },
    {
      name: "dog",
    },
    {
      name: "lizard",
    },
    {
      name: "snake",
    },
    {
      name: "bird",
    },
    {
      name: "hamster",
    },
  ],
  petTypes: "\\{{$pickSome(allPetTypes)}}\\",
  
}
```

#### Script

```js
const petTypePromises = jc.variables.get("petTypes").map(petType =>
    jc.sendRequestAsync("Create a pet type", withJsonBody(petType))
        .then(response => {
            response.to.have.status(201)
            const responseBody = response.json()
            jc.expect(responseBody).to.have.property("id")

            const petTypeWithoutId = _.omit(responseBody, 'id')

            jc.expect(petTypeWithoutId).to.deep.equal(petType)
            return responseBody
        })
)

return await Promise.all(petTypePromises)

```
