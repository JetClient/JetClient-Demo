```toml
name = 'Delete all data'
sortWeight = 2000000
id = '4a8e0af5-c3c9-42db-be8e-e6c754249d8c'
```

#### Script

```js
jc.runTestSuite('/petclinic/visit/Delete visits')

jc.runTestSuite('/petclinic/pet/Delete pets')

jc.runTestSuite('/petclinic/owner/Delete owners')

jc.runTestSuite('/petclinic/vet/Delete vets')

jc.runTestSuite('/petclinic/specialty/Delete specialties')

jc.runTestSuite('/petclinic/pettypes/Delete pet types')

```
