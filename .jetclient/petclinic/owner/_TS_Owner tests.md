```toml
name = 'Owner tests'
sortWeight = 3000000
id = '6a12cea9-ff58-41c6-912e-48363e331c20'
```

#### Script

```js
function randomOwner() {
    return _.sample(jc.variables.get("ownersWithIds"))
}

function withOwnerId(id) {
    return request => request.setPathVariables({ ownerId: id })
}

jc.testCase("Setup", () => {
    jc.runScript('Delete owners')
    const createdOwners = jc.runScript('Create owners')

    jc.expect(createdOwners).to.not.be.empty
    jc.scriptVariables.set("ownersWithIds", createdOwners)
})

jc.testCase("Lists pet owners", () => {
    const response = jc.sendRequest("Lists pet owners")
    response.to.have.status(200)
    const listedOwners = response.json()
    jc.expect(listedOwners).to.not.be.empty

    const createdOwners = jc.variables.get("ownersWithIds")
    jc.expect(listedOwners).to.have.deep.members(createdOwners)
})

jc.testCase("Create owner error", () => {
    const badOwner = {
        lastName: "Doe",
        address: "123 Main St",
        city: "Anytown",
        telephone: "1234567890"
        // Missing firstName
    }

    const response = jc.sendRequest("Adds a pet owner", req =>
        req.setBodyJson(badOwner)
    )
    response.to.have.status(400)
})

jc.testCase("Retrieve owner by ID", () => {
    const owner = randomOwner()

    const response = jc.sendRequest("Get a pet owner by ID", withOwnerId(owner.id))
    response.to.have.status(200)
    jc.expect(response.json()).to.deep.equal(owner)
})

jc.testCase("Update owner", () => {
    const ownerId = randomOwner().id
    const updatedOwner = {
        firstName: "Jane",
        lastName: "Doe",
        address: "456 Elm St",
        city: "New City",
        telephone: "9876543210"
    }

    const response = jc.sendRequest("Update a pet owner's details", req =>
        req.setPathVariables({ ownerId })
            .setBodyJson(updatedOwner)
    )
    response.to.have.status(204)

    const verifyResponse = jc.sendRequest("Get a pet owner by ID", withOwnerId(ownerId))
    verifyResponse.to.have.status(200)

    const expectedOwner = { id: ownerId, pets: [], ...updatedOwner }
    jc.expect(verifyResponse.json()).to.deep.equal(expectedOwner)
})

jc.testCase("Delete owner", () => {
    const ownerId = randomOwner().id

    const response = jc.sendRequest("Delete an owner by ID", withOwnerId(ownerId))
    response.to.have.status(204)

    const verifyResponse = jc.sendRequest("Get a pet owner by ID", withOwnerId(ownerId))
    verifyResponse.to.have.status(404)
})

jc.testCase("Teardown", () => {
    jc.runScript('Delete owners')
    jc.scriptVariables.clear()
})

```
