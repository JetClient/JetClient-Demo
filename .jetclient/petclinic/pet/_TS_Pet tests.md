```toml
name = 'Pet tests'
sortWeight = 3000000
id = 'b7bf9240-7ca3-4067-a68d-0621362a4218'
```

#### Script

```js
function randomPet() {
    return _.sample(jc.variables.get("petsWithIds"))
}

function withPetId(id) {
    return request => request.setPathVariables({petId: id})
}

jc.testCase("Setup", () => {
    jc.runTestSuite('Delete pets')
    jc.runTestSuite('/petclinic/owner/Delete owners')
    jc.runTestSuite('/petclinic/pettypes/Delete pet types')
    const createdPets = jc.runTestSuite('Create pets')

    jc.expect(createdPets).to.not.be.empty
    jc.testSuiteVariables.set("petsWithIds", createdPets)
})

jc.testCase("Create pet error", () => {
    const badPet = {
        name: "Buddy",
        birthDate: "2023-01-01"
        // Missing ownerId and type
    }

    const response = jc.sendRequest("Adds a pet to an owner", req =>
        req.setBodyJson(badPet)
    )
    response.to.have.status(400)
})

jc.testCase("Retrieve pet by ID", () => {
    const pet = randomPet()

    const response = jc.sendRequest("Get a pet by ID", withPetId(pet.id))
    response.to.have.status(200)
    jc.expect(response.json()).to.deep.equal(pet)
})

jc.testCase("Update pet", () => {
    const pet = randomPet()
    const petId = pet.id
    const updatedPet = {
        name: "Updated Pet",
        birthDate: "2024-01-01",
        type: pet.type,
        ownerId: pet.ownerId
    }

    const response = jc.sendRequest("Update a pet by ID", req =>
        req.setPathVariables({petId})
            .setBodyJson(updatedPet)
    )
    response.to.have.status(204)

    const verifyResponse = jc.sendRequest("Get a pet by ID", withPetId(petId))
    verifyResponse.to.have.status(200)

    const expectedPet = {id: petId, visits: [], ...updatedPet}
    jc.expect(verifyResponse.json()).to.deep.equal(expectedPet)
})

jc.testCase("Delete pet", () => {
    const petId = randomPet().id

    const response = jc.sendRequest("Delete a pet by ID", withPetId(petId))
    response.to.have.status(204)

    const verifyResponse = jc.sendRequest("Get a pet by ID", withPetId(petId))
    verifyResponse.to.have.status(404)
})

jc.testCase("Teardown", () => {
    jc.runTestSuite('Delete pets')
    jc.runTestSuite('/petclinic/owner/Delete owners')
    jc.runTestSuite('/petclinic/pettypes/Delete pet types')
    jc.testSuiteVariables.clear()
})
```
