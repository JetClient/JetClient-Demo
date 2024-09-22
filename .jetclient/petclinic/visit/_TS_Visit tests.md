```toml
name = 'Visit tests'
sortWeight = 3000000
id = '7873979f-e634-4ecd-8a97-db36ae0c958f'
```

#### Script

```js
function randomVisit() {
    return _.sample(jc.testSuiteVariables.get("visits"))
}

function withVisitId(id) {
    return request => request.setPathVariables({visitId: id})
}

jc.testCase("Setup", async () => {
    jc.runTestSuite('Delete visits')
    jc.runTestSuite('/petclinic/pet/Delete pets')
    jc.runTestSuite('/petclinic/owner/Delete owners')
    jc.runTestSuite('/petclinic/pettypes/Delete pet types')

    const createdVisits = jc.runTestSuite('Create visits')
    jc.expect(createdVisits).to.not.be.empty

    jc.testSuiteVariables.set("visits", createdVisits)
})

jc.testCase("Lists visits", () => {
    const response = jc.sendRequest("Lists visits")
    response.to.have.status(200)
    const listedVisits = response.json()
    jc.expect(listedVisits).to.not.be.empty

    const createdVisits = jc.testSuiteVariables.get("visits")
    jc.expect(listedVisits).to.have.deep.members(createdVisits)
})

jc.testCase("Create visit error", () => {
    const badVisit = {
        date: "2023-01-01",
        description: "Routine Checkup"
        // Missing petId
    }

    const response = jc.sendRequest("Adds a vet visit", req =>
        req.setBodyJson(badVisit)
    )
    response.to.have.status(400)
})

jc.testCase("Retrieve visit by ID", () => {
    const visit = randomVisit()

    const response = jc.sendRequest("Get a visit by ID", withVisitId(visit.id))
    response.to.have.status(200)
    jc.expect(response.json()).to.deep.equal(visit)
})

jc.testCase("Update visit", () => {
    const visit = randomVisit()
    const visitId = visit.id
    const updatedVisit = {
        date: "2024-01-01",
        description: "Updated Checkup",
        petId: visit.petId
    }

    const response = jc.sendRequest("Update a visit by ID", req =>
        req.setPathVariables({visitId})
            .setBodyJson(updatedVisit)
    )
    response.to.have.status(204)

    const verifyResponse = jc.sendRequest("Get a visit by ID", withVisitId(visitId))
    verifyResponse.to.have.status(200)

    const expectedVisit = {id: visitId, ...updatedVisit}
    jc.expect(verifyResponse.json()).to.deep.equal(expectedVisit)
})

jc.testCase("Delete visit", () => {
    const visitId = randomVisit().id

    const response = jc.sendRequest("Delete a visit by ID", withVisitId(visitId))
    response.to.have.status(204)

    const verifyResponse = jc.sendRequest("Get a visit by ID", withVisitId(visitId))
    verifyResponse.to.have.status(404)
})

jc.testCase("Teardown", () => {
    jc.runTestSuite('Delete visits')
    jc.runTestSuite('/petclinic/pet/Delete pets')
    jc.runTestSuite('/petclinic/owner/Delete owners')
    jc.runTestSuite('/petclinic/pettypes/Delete pet types')
})

```
