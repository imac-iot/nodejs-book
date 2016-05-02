#模組
- ES5

```javascript
//module.js
module.exports = {
  echo : function(){
    console.log('test');
  },
}

//app.js
var module = require('./module');
module.echo();

```

- ES6

```javascript
//module.js
export function add(a, b) {
  return a + b;
}

export function mult(a, b) {
  return a * b;
}

//app.js

//逐一加載
import { add, mult } form './module';

console.log('加法： ' + add(2, 3));
console.log('乘法： ' + mult(1, 3));

//整體加載
import * as math from './module';

console.log('加法： ' + math.add(1, 2));
console.log('乘法： ' + math.mult(1, 2));

```