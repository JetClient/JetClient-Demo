```toml
name = 'Vet tests'
sortWeight = 3000000
id = 'e66a9b0a-059c-4e84-bc5d-c11ecce9e758'
```

#### Script

```js
function randomVet() {
    return _.sample(jc.variables.get("vets"))
}

function withId(id) {
    return request => request.setPathVariables({vetId: id})
}

jc.testCase("Setup", () => {
    jc.runTestSuite('Delete vets')
    const createdVets = jc.runTestSuite('Create vets')

    jc.expect(createdVets).to.not.be.empty
    jc.testSuiteVariables.set("vets", createdVets)
})

jc.testCase("Lists vets", () => {
    const response = jc.sendRequest("Lists vets")
    response.to.have.status(200)
    const listedVets = response.json()
    jc.expect(listedVets).to.not.be.empty

    const createdVets = jc.variables.get("vets")
    jc.expect(listedVets).to.have.deep.members(createdVets)
})

jc.testCase("Create vet error", () => {
    const invalidVets = [
        {lastName: "Doe"},
        {firstName: "John"},
        {}
    ]

    for (const badVet of invalidVets) {
        const response = jc.sendRequest("Create a Vet", withJsonBody(badVet))
        response.to.have.status(400)
    }
})

jc.testCase("Retrieve vet by ID", () => {
    const vet = randomVet()
    const response = jc.sendRequest("Get a vet by ID", withId(vet.id))
    response.to.have.status(200)
    jc.expect(response.json()).to.deep.equal(vet)
})

jc.testCase("Update vet", () => {
    const vetId = randomVet().id
    const updatedVet = {
        firstName: "Jane",
        lastName: "Doe",
        specialties: []
    }

    const updateResponse = jc.sendRequest("Update a vet by ID", req =>
        req.setPathVariables({vetId})
            .setBodyJson(updatedVet)
    )
    updateResponse.to.have.status(204)

    const verifyResponse = jc.sendRequest("Get a vet by ID", withId(vetId))
    verifyResponse.to.have.status(200)
    const expectedVet = {id: vetId, ...updatedVet}
    jc.expect(verifyResponse.json()).to.deep.equal(expectedVet)
})

jc.testCase("Delete vet", () => {
    const vetId = randomVet().id

    const deleteResponse = jc.sendRequest("Delete a vet by ID", withId(vetId))
    deleteResponse.to.have.status(204)

    const verifyResponse = jc.sendRequest("Get a vet by ID", withId(vetId))
    verifyResponse.to.have.status(404)
})

jc.testCase("Teardown", () => {
    jc.runTestSuite('Delete vets')
})

```
