#### Util:

###### Current year:
```
const year = new Date().toISOString().slice(0, 4);
```



###### Object Length:
```
Object.keys(check).length;
```


#### Add More:
```
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
```

#### Validation:
* Remove validation:
* ```
  "data.is_former"(current, old) {
      if (current !== old) {
        this.validation.reset(); <----
      }
    },
  ```
