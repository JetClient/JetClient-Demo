```toml
name = 'Using Faker.js'
sortWeight = 6000000
id = '25881422-30c1-4593-8660-181f63be2914'
```

#### Script

```js
// Run `npm install` in the .jetclient/library folder

faker = require('@faker-js/faker/dist/cjs/locale/en').faker

function createRandomUser (){
    return {
        userId: faker.string.uuid(),
        username: faker.internet.userName(),
        email: faker.internet.email(),
        avatar: faker.image.avatar(),
        password: faker.internet.password(),
        birthdate: faker.date.birthdate(),
        registeredAt: faker.date.past(),
    }
}

console.log(createRandomUser())
```
