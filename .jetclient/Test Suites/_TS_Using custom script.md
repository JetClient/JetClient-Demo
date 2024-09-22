```toml
name = 'Using custom script'
sortWeight = 5000000
id = '53982a3d-26ee-4b38-9452-0ab83b1f0645'
```

#### Script

```js
const utils = require('./utils.js');

const randomInt = utils.getRandomInt(1, 2)
console.log(`Random integer between 1 and 100: ${randomInt}`);

const today = new Date();
const formattedDate = utils.formatDate(today);
console.log(`Today's date formatted: ${formattedDate}`);

const originalString = 'hello world';
const capitalizedString = utils.capitalizeFirstLetter(originalString);
console.log(`Capitalized string: ${capitalizedString}`);
```
