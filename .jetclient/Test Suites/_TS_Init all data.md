```toml
name = 'Init all data'
sortWeight = 3000000
id = '12528354-e236-4742-a87e-2dcf18d50fa6'
```

#### Script

```js
jc.runScript('/petclinic/specialty/Create specialties')

jc.runScript('/petclinic/vet/Create vets')

jc.runScript('/petclinic/pettypes/Create pet types')

jc.runScript('/petclinic/owner/Create owners')

jc.runScript('/petclinic/pet/Create pets')

jc.runScript('/petclinic/visit/Create visits')
```
