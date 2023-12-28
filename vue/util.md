#### Util:

###### Use of window:
 
window.variableName means that the variable is being declared at the global scope.

```js
window.baseurl = "/";
```

###### The $

```js
$root = The main app.js or index.js where vue is initiate!

``

###### Current year:

```js
const year = new Date().toISOString().slice(0, 4); 

```

###### Object Length:

```js
Object.keys(check).length; 

```

###### Add More:

```js
// Formula 01:

// Vue SFC:
<button @click="
data.length.push({
  duration: '', 
}) "
  class="btn btn-sm btn-primary float-right"
  type="button"

> Add More </button>

// Remove script:
removeItem(id) {
 this.data.length.splice(id, 1); 
}, 

```js
###### Validation:

* Remove validation:
* ```

  "data.is_former"(current, old) {

      if (current !== old) {
        this.validation.reset(); <----
      }
    },

  ```
