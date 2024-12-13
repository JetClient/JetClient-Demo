```toml
name = 'All tests'
sortWeight = 4000000
id = '0c3acb3d-c708-4cf5-ab93-2f86da2eb43f'
```

#### Variables

```json5
{
  testSuitesToRun: {
    owner: "\\{{$checkBoxInput('Owner tests', true)}}\\",
    pet: "\\{{$checkBoxInput('Pet tests', true)}}\\",
    visit: "\\{{$checkBoxInput('Visit tests', true)}}\\",
    petType: "\\{{$checkBoxInput('Pet Type tests', true)}}\\",
    specialty: "\\{{$checkBoxInput('Specialty tests', true)}}\\",
    vet: "\\{{$checkBoxInput('Vet tests', true)}}\\",
    user: "\\{{$checkBoxInput('User tests', true)}}\\",
  }
}
```

#### Script

```js
jc.runTestSuite('Delete all data')

const testSuitesToRun = jc.variables.get('testSuitesToRun')

if (testSuitesToRun.owner) {
    jc.runTestSuite('/petclinic/owner/Owner tests')
}
if (testSuitesToRun.pet) {
    jc.runTestSuite('/petclinic/pet/Pet tests')
}
if (testSuitesToRun.visit) {
    jc.runTestSuite('/petclinic/visit/Visit tests')
}
if (testSuitesToRun.pettype) {
    jc.runTestSuite('/petclinic/pettypes/Pet type tests')
}
if (testSuitesToRun.specialty) {
    jc.runTestSuite('/petclinic/specialty/Specialty tests')
}
if (testSuitesToRun.vet) {
    jc.runTestSuite('/petclinic/vet/Vet tests')
}
if (testSuitesToRun.user) {
    jc.runTestSuite('/petclinic/user/User Tests')
}
```
