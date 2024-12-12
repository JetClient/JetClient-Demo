```toml
name = 'Specialty tests'
sortWeight = 3000000
id = 'f5b2a61b-dca8-46c4-89c1-65d5a8a92f21'
```

#### Script

```js
function randomSpecialty() {
    return _.sample(jc.variables.get("specialties"))
}

function withId(id) {
    return request => request.setPathVariables({ specialtyId: id })
}

jc.testCase("Setup", () => {
    jc.runTestSuite('Delete specialties')
    const createdSpecialties = jc.runTestSuite('Create specialties')

    jc.expect(createdSpecialties).to.not.be.empty
    jc.testSuiteVariables.set("specialties", createdSpecialties)
})

jc.testCase("Lists specialties", () => {
    const response = jc.sendRequest("Lists specialties")
    response.to.have.status(200)
    const listedSpecialties = response.json()
    jc.expect(listedSpecialties).to.not.be.empty

    const createdSpecialties = jc.variables.get("specialties")
    jc.expect(listedSpecialties).to.have.deep.members(createdSpecialties)
})

jc.testCase("Create specialty error", () => {
    const badSpecialty = {}

    const response = jc.sendRequest("Create a specialty", req =>
        req.setBodyJson(badSpecialty)
    )
    response.to.have.status(400)
})

jc.testCase("Retrieve specialty by ID", () => {
    const specialty = randomSpecialty()

    const response = jc.sendRequest("Get a specialty by ID", withId(specialty.id))
    response.to.have.status(200)
    jc.expect(response.json()).to.deep.equal(specialty)
})

jc.testCase("Update specialty", () => {
    const specialtyId = randomSpecialty().id
    const updatedSpecialty = {
        name: "Updated Specialty"
    }

    const updateResponse = jc.sendRequest("Update a specialty by ID", req =>
        req.setPathVariables({ specialtyId })
            .setBodyJson(updatedSpecialty)
    )
    updateResponse.to.have.status(204)

    const verifyResponse = jc.sendRequest("Get a specialty by ID", withId(specialtyId))
    verifyResponse.to.have.status(200)

    const expectedSpecialty = { id: specialtyId, ...updatedSpecialty }
    jc.expect(verifyResponse.json()).to.deep.equal(expectedSpecialty)
})

jc.testCase("Delete specialty", () => {
    const specialtyId = randomSpecialty().id

    const deleteResponse = jc.sendRequest("Delete a specialty by ID", withId(specialtyId))
    deleteResponse.to.have.status(204)

    const verifyResponse = jc.sendRequest("Get a specialty by ID", withId(specialtyId))
    verifyResponse.to.have.status(404)
})

jc.testCase("Teardown", () => {
    jc.runTestSuite('Delete specialties')
})

```
