```toml
name = 'Create vets'
sortWeight = 1000000
id = '1b1e4b89-9f97-4d1e-bee3-2a1c2adff1e2'
```

#### Variables

```json5
{
  $vet: {
    firstName: '{{$randomFirstName}}',
    lastName: '{{$randomLastName}}'
  },
  vets: "\\{{$repeat($vet, $randomInt(10, 20))}}\\"
}

```

#### Script

```js
function getExistingSpecialties() {
    const response = jc.sendRequest('/petclinic/specialty/Lists specialties')
    if (response.code !== 404) {
        const specialties = response.json()
        if (specialties.length > 0) {
            return specialties
        }
    }
    return null
}

const specialties = getExistingSpecialties() || jc.runTestSuite('/petclinic/specialty/Create specialties')
jc.expect(specialties).to.not.be.empty

function getRandomSpecialties(specialties) {
    const count = _.random(0, 2)
    return _.sampleSize(specialties, count)
}

const vetPromises = jc.variables.get("vets")
    // Filter out vets with non-alphabetic first and last names because the API doesn't accept them
    .filter(owner => /^[A-Za-z]+$/.test(owner.firstName) && /^[A-Za-z]+$/.test(owner.lastName))
    .map(vet => {
        const randomSpecialties = getRandomSpecialties(specialties)
        const vetWithSpecialties = {
            ...vet,
            specialties: randomSpecialties.map(s => _.omit(s, 'id'))
        }

        return jc.sendRequestAsync("Create a Vet", withJsonBody(vetWithSpecialties))
            .then(response => {
                response.to.have.status(201)
                const responseBody = response.json()
                jc.expect(responseBody).to.have.property("id")

                const vetWithoutIds = _.omit(responseBody, 'id')
                vetWithoutIds.specialties = responseBody.specialties.map(specialty =>
                    _.omit(specialty, 'id')
                )

                const expectedSpecialties = new Set(vetWithSpecialties.specialties.map(s => JSON.stringify(s)))
                const actualSpecialties = new Set(vetWithoutIds.specialties.map(s => JSON.stringify(s)))

                const isSubset = [...expectedSpecialties].every(s => actualSpecialties.has(s))

                jc.expect(isSubset).to.be.true
                return responseBody
            })
            .catch(error => {
                console.error("Error creating vet:", error)
                throw error
            })
    })

return await Promise.all(vetPromises)

```
