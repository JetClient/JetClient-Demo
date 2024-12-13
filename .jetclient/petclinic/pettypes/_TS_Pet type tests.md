```toml
name = 'Pet type tests'
sortWeight = 3000000
id = '2b89c4aa-5568-4c5a-8d8b-823e4ee8e8d7'
```

#### Script

```js
function randomPetType() {
    return _.sample(jc.variables.get("petTypesWithIds"))
}

function withPetTypeId(id) {
    return request => request.setPathVariables({ petTypeId: id })
}

jc.testCase("Setup", () => {
    jc.runTestSuite('Delete pet types')
    const createdPetTypes = jc.runTestSuite('Create pet types')

    jc.expect(createdPetTypes).to.not.be.empty
    jc.testSuiteVariables.set("petTypesWithIds", createdPetTypes)
})

jc.testCase("Lists pet types", () => {
    const response = jc.sendRequest("Lists pet types")
    response.to.have.status(200)
    const listedPetTypes = response.json()
    jc.expect(listedPetTypes).to.not.be.empty

    const createdPetTypes = jc.variables.get("petTypesWithIds")
    jc.expect(listedPetTypes).to.have.deep.members(createdPetTypes)
})

jc.testCase("Create pet type error", () => {
    const badPetType = {} // Missing name

    const response = jc.sendRequest("Create a pet type", req =>
        req.setBodyJson(badPetType)
    )
    response.to.have.status(400)
})

jc.testCase("Retrieve pet type by ID", () => {
    const petType = randomPetType()

    const response = jc.sendRequest("Get a pet type by ID", withPetTypeId(petType.id))
    response.to.have.status(200)
    jc.expect(response.json()).to.deep.equal(petType)
})

jc.testCase("Update pet type", () => {
    const petTypeId = randomPetType().id
    const updatedPetType = {
        name: "Updated Pet Type",
        id: petTypeId
    }

    const updateResponse = jc.sendRequest("Update a pet type by ID", req =>
        req.setPathVariables({ petTypeId })
            .setBodyJson(updatedPetType)
    )
    updateResponse.to.have.status(204)

    const verifyResponse = jc.sendRequest("Get a pet type by ID", withPetTypeId(petTypeId))
    verifyResponse.to.have.status(200)

    const expectedPetType = { id: petTypeId, ...updatedPetType }
    jc.expect(verifyResponse.json()).to.deep.equal(expectedPetType)
})

jc.testCase("Delete pet type", () => {
    const petTypeId = randomPetType().id

    const deleteResponse = jc.sendRequest("Delete a pet type by ID", withPetTypeId(petTypeId))
    deleteResponse.to.have.status(204)

    const verifyResponse = jc.sendRequest("Get a pet type by ID", withPetTypeId(petTypeId))
    verifyResponse.to.have.status(404)
})

jc.testCase("Teardown", () => {
    jc.runTestSuite('Delete pet types')
    jc.testSuiteVariables.clear()
})

```
