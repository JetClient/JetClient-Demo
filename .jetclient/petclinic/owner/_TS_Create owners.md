```toml
name = 'Create owners'
sortWeight = 1000000
id = '52214264-cc5c-46ec-a30e-1e09fbc23112'
```

#### Variables

```json5
{
  owners: [
    {
      firstName: "George",
      lastName: "Franklin",
      address: "110 W. Liberty St.",
      city: "Madison",
      telephone: "6085551023",
    },
    {
      firstName: "Betty",
      lastName: "Davis",
      address: "638 Cardinal Ave.",
      city: "Sun Prairie",
      telephone: "6085551749",
    },
    {
      firstName: "Eduardo",
      lastName: "Rodriquez",
      address: "2693 Commerce St.",
      city: "McFarland",
      telephone: "6085558763",
    },
    {
      firstName: "Harold",
      lastName: "Davis",
      address: "563 Friendly St.",
      city: "Windsor",
      telephone: "6085553198",
    },
    {
      firstName: "Peter",
      lastName: "McTavish",
      address: "2387 S. Fair Way",
      city: "Madison",
      telephone: "6085552765",
    },
    {
      firstName: "Jean",
      lastName: "Coleman",
      address: "105 N. Lake St.",
      city: "Monona",
      telephone: "6085552654",
    },
    {
      firstName: "Jeff",
      lastName: "Black",
      address: "1450 Oak Blvd.",
      city: "Monona",
      telephone: "6085555387",
    },
    {
      firstName: "Maria",
      lastName: "Escobito",
      address: "345 Maple St.",
      city: "Madison",
      telephone: "6085557683",
    },
    {
      firstName: "David",
      lastName: "Schroeder",
      address: "2749 Blackhawk Trail",
      city: "Madison",
      telephone: "6085559435",
    },
    {
      firstName: "Carlos",
      lastName: "Estaban",
      address: "2335 Independence La.",
      city: "Waunakee",
      telephone: "6085555487",
    }
  ]
}

```

#### Script

```js
const ownerPromises = jc.testSuiteVariables.get("owners").map(owner =>
    jc.sendRequestAsync("Adds a pet owner", withJsonBody(owner))
        .then(response => {
            response.to.have.status(201)
            const responseBody = response.json()
            jc.expect(responseBody).to.have.property("id")

            const ownerWithoutIdAndPets = _.omit(responseBody, 'id', 'pets')

            jc.expect(ownerWithoutIdAndPets).to.deep.equal(owner)
            return responseBody
        })
)

return await Promise.all(ownerPromises)

```
