```toml
name = 'Create pets'
sortWeight = 1000000
id = '32a5595c-e2f6-4b51-ac16-2f5fd427ceb3'
```

#### Variables

```json5
{
  $pet: {
    name: "{{$randomFirstName}}",
    birthDate: "\\{{$randomBirthdate}}\\"
  },
  pets: "\\{{$repeat($pet, $randomInt(10, 20))}}\\"
}
```

#### Script

```js
function getExistingOwners() {
    const response = jc.sendRequest('/petclinic/owner/Lists pet owners')
    if (response.code !== 404) {
        const owners = response.json()
        if (owners.length > 0) {
            return owners
        }
    }
    return null
}

function getExistingPetTypes() {
    const response = jc.sendRequest('/petclinic/pettypes/Lists pet types')
    if (response.code !== 404) {
        const petTypes = response.json()
        if (petTypes.length > 0) {
            return petTypes
        }
    }
    return null
}

const owners = getExistingOwners() || jc.runScript('/petclinic/owner/Create owners')
jc.expect(owners).to.not.be.empty

const petTypes = getExistingPetTypes() || jc.runScript('/petclinic/pettypes/Create pet types')
jc.expect(petTypes).to.not.be.empty

const randomOwnerId = () => _.sample(owners).id
const randomPetType = () => _.sample(petTypes)

const petPromises = jc.variables.get("pets").map(pet => {
    const ownerId = randomOwnerId()
    const petType = randomPetType()
    const petWithType = { ...pet, ownerId, type: petType }

    return jc.sendRequestAsync("Adds a pet to an owner", req =>
        req.setBodyJson(petWithType)
            .setPathVariables({ ownerId })
    )
        .then(response => {
            response.to.have.status(201)
            const responseBody = response.json()
            jc.expect(responseBody).to.have.property("id")

            const petWithoutIdAndVisits = _.omit(responseBody, 'id', 'visits')
            jc.expect(petWithType).to.deep.equal(petWithoutIdAndVisits)
            return responseBody
        })
        .catch(error => {
            console.error("Error adding pet:", error)
            throw error
        })
})

return await Promise.all(petPromises)

```
