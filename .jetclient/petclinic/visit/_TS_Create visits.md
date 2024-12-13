```toml
name = 'Create visits'
sortWeight = 1000000
id = 'd8fd9ee2-890e-4f7e-9702-1e2dc755f30a'
```

#### Variables

```json5
{
  $visit: {
    date: "{{$randomPastDate}}",
    description: "{{$randomLoremSentence}}"
  },
  visits: "\\{{$repeat($visit, $randomInt(10, 20))}}\\"
}
```

#### Script

```js
function getExistingPets() {
    const response = jc.sendRequest('/petclinic/pet/Lists pet')
    if (response.code !== 404) {
        const pets = response.json()
        if (pets.length > 0) {
            return pets
        }
    }
    return null
}

const pets = getExistingPets() || jc.runTestSuite('/petclinic/pet/Create pets')
jc.expect(pets).to.not.be.empty

const visitPromises = jc.variables.get("visits").map(visit => {
    const pet = _.sample(pets)
    const petId = pet.id
    const visitWithPetId = { ...visit, petId }

    return jc.sendRequestAsync("Adds a vet visit", req =>
        req.setBodyJson(visitWithPetId)
            .setPathVariables({ petId, ownerId: pet.ownerId })
    )
        .then(response => {
            response.to.have.status(201)
            const responseBody = response.json()
            jc.expect(responseBody).to.have.property("id")

            const visitWithoutId = _.omit(responseBody, 'id')
            jc.expect(visitWithPetId).to.deep.equal(visitWithoutId)
            return responseBody
        })
        .catch(error => {
            console.error("Error creating visit:", error)
            throw error
        })
})

return await Promise.all(visitPromises)

```
