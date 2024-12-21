```toml
name = 'Delete all data'
sortWeight = 2000000
id = '4a8e0af5-c3c9-42db-be8e-e6c754249d8c'
```

#### Script

```js
jc.runScript('/petclinic/visit/Delete visits')

jc.runScript('/petclinic/pet/Delete pets')

jc.runScript('/petclinic/owner/Delete owners')

jc.runScript('/petclinic/vet/Delete vets')

jc.runScript('/petclinic/specialty/Delete specialties')

jc.runScript('/petclinic/pettypes/Delete pet types')

```
