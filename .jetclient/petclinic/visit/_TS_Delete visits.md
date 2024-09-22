```toml
name = 'Delete visits'
sortWeight = 2000000
id = '4603e172-0613-4563-8246-a630267de359'
```

#### Script

```js
const listVisitsResponse = await jc.sendRequestAsync("Lists visits")
const visitIds = listVisitsResponse.code === 404 ? [] : listVisitsResponse.json("$[*].id")

for (let visitId of visitIds) {
    const response = await jc.sendRequestAsync('Delete a visit by ID', req =>
        req.setPathVariables({visitId})
    )
    jc.expect(response.code).to.be.oneOf([204, 404])
}

```
