```toml
name = 'Create owners'
sortWeight = 1000000
id = '52214264-cc5c-46ec-a30e-1e09fbc23112'
```

#### Variables

```json5
{
  $owner: {
    firstName: "{{$randomFirstName}}",
    lastName: "{{$randomLastName}}",
    address: "{{$randomStreetAddress}}",
    city: "{{$randomCity}}",
    telephone: "{{$randomPhoneNumber('##########')}}",
  },
  owners: "\\{{$repeat($owner, $randomInt(10, 20))}}\\"
}
```

#### Script

```js
const ownerPromises = jc.variables.get("owners")
    // Filter out owners with non-alphabetic first and last names because the API doesn't accept them
    .filter(owner => /^[A-Za-z]+$/.test(owner.firstName) && /^[A-Za-z]+$/.test(owner.lastName))
    .map(owner =>
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
