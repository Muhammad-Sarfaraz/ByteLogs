# Hands on Note for Javascript

#### Data-Types: 
There are 7 data-types as of ECMAScript 2020.
| Data Types  | Examples                                                              |
| ----------- | --------------------------------------------------------------------- |
| `undefined` | A variable that has not been assigned a value is of type `undefined`. |
| `null`      | no value.                                                             |
| `string`    | `'a', 'aa', 'aaa', 'Hello!', '11 cats'`                               |
| `number`    | `12, -1, 0.4`                                                         |
| `boolean`   | `true, false`                                                         |
| `object`    | A collection of properties.                                           |
| `symbol`    | Represents a unique identifier.                                       |

####  ES6 var, let and const:
* Unlike var, let throws an error if you declare the same variable twice.
* Variables declared with const are read-only and cannot be reassigned.
* Objects (including arrays and functions) assigned to a variable using const are still mutable and only prevents the reassignment of the variable identifier.


* Object freeze:
```
let obj = {
  name: "john Abraham Khan",
age: "40",
};

Object.freeze(obj);
```

#### String:
* Concatenation:
  ```
  var str = "One. " + "Two.";
  ```
* Length of a string:
   ```
  "Abraham Khan".length;
  ```

#### Module:

###### Export:
```
// Type 01:
const score = function(){
    return 100;
}

export default score;

// Type 02:
const score = 100;
const time = 40s;

export {score, time};
```

###### Import:
* Type 01: Import multiple function:
```
import {score,time} from "./script/top.js";
```
* Type 02: Only import the default function:

 ```
import score from "./script/bar.js";
```
* Type 03: Import every public function from module:

```
import * as board from './score';
```

* Use case:
```
alert(score,time);
alert(score());
```


#### ES5:

#### ES6:

#### Util Function:

###### Array to String:
```
arrayToString(value) {
  var string = Object.entries(value);
  var arrayToString = string.map((entry) => entry[1]).join(",");
  return arrayToString;
},
```

###### Scroll To Top:
```
 scrollTop(x = 0, y = 0) {
      window.scrollTo(x, y)
},
```

###### Breadcrum Format [routePate -> Route Path]:
```
// Make pascal to breadcrumb format.
breadcrumbFormat(str) {
      return str.replace(/([A-Z])/g, ' $1').trim();
},
```

###### Ucfirst:
```
// Alternative of php's ucfirst.
ucfirst(str) {
      if (typeof str !== 'string' || str.length === 0) {
          return str;
      }

      return str.charAt(0).toUpperCase() + str.slice(1);
},

```


#### The Array Loop Hole:


###### Push:
```
types() {
  const types = [];
  if (Object.keys(this.designationTypes).length > 0) {
    this.designationTypes.forEach(function (type) {
      types.push({
        name: type.name,
        value: type.value,
      });
    });
  }
  return types;
},
```

#### Networking:

###### xhr :
```
const url = 'https://api.example.com/data';
const data = { username: 'JohnDoe', password: 'secretpassword' };

const xhr = new XMLHttpRequest();
xhr.open('POST', url);
xhr.setRequestHeader('Content-Type', 'application/json');

xhr.onload = function() {
  if (xhr.status === 200) {
    const responseData = JSON.parse(xhr.responseText);
    // Handle the response data
    console.log(responseData);
  } else {
    // Handle the error
    console.error('Error:', xhr.status);
  }
};

xhr.onerror = function() {
  // Handle any network errors
  console.error('Network Error');
};

xhr.send(JSON.stringify(data));

```

###### Post:
```
const url = 'https://api.example.com/data';
const data = { username: 'JohnDoe', password: 'secretpassword' };

fetch(url, {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json'
  },
  body: JSON.stringify(data)
})
  .then(response => {
    if (!response.ok) {
      throw new Error('Network response was not ok');
    }
    return response.json();
  })
  .then(responseData => {
    // Handle the response data
    console.log(responseData);
  })
  .catch(error => {
    // Handle any errors that occurred during the request
    console.error('Error:', error);
  });
``` 

###### Get:
```
fetch('https://api.example.com/data')
  .then(response => {
    if (!response.ok) {
      throw new Error('Network response was not ok');
    }
    return response.json();
  })
  .then(data => {
    // Handle the data received from the server
    console.log(data);
  })
  .catch(error => {
    // Handle any errors that occurred during the request
    console.error('Error:', error);
  });
```
