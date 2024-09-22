```toml
name = 'Init all data'
sortWeight = 3000000
id = '12528354-e236-4742-a87e-2dcf18d50fa6'
```

#### Script

```js
jc.runTestSuite('/petclinic/specialty/Create specialties')

jc.runTestSuite('/petclinic/vet/Create vets')

jc.runTestSuite('/petclinic/pettypes/Create pet types')

jc.runTestSuite('/petclinic/owner/Create owners')

jc.runTestSuite('/petclinic/pet/Create pets')

jc.runTestSuite('/petclinic/visit/Create visits')
```
