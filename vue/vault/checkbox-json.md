# Checkbox Json

#### Checkbox will contain json value.

``` json ```
```json
{
  "field_name":"a",
  "type":"input",
  "title":"A"
}
```

``` controller ```
```php
$data = $request->all();
$data['json'] = "[" . $request->json . "]"; // Add this, json array!
```

``` vue.js ```
```js
<div v-for="(checkbox, index) in inputSettings" :key="index">
    <input
      type="checkbox"
      :name="'json[' + index + ']'"
      :value="JSON.stringify(checkbox)"
      :checked="isChecked(checkbox, index)"
      v-on:change="updateCheckedValue(index)"
    />
    {{ checkbox.title }}
    <br />
</div>

methods:{
store(){
  var form = document.getElementById("form");
  var formData = new FormData(form);
  formData.append("json", this.selectedValues);
},
isChecked(value, index) {
  let isChecked = false;
  if (this.selectedValues && this.selectedValues.length > 0) {
    this.selectedValues.forEach((element) => {
      const item = JSON.parse(element);
      if (value.field_name == item.field_name) {
        isChecked = true;
      }
    });
  }
  return isChecked;
},
updateCheckedValue(index) {
  const selectedValue = JSON.stringify(this.$root.inputSettings[index]);
  const indexInSelectedValues = this.selectedValues.indexOf(selectedValue);
  
  if (indexInSelectedValues === -1) {
    this.selectedValues.push(selectedValue);
  } else {
    this.selectedValues.splice(indexInSelectedValues, 1);
  }
},

}
created(){
  // Inside the api request!
  if (res.data.json) {
    const jsonString = res.data.json;
    const jsonArray = JSON.parse(jsonString);
    this.selectedValues = jsonArray.map((item) => JSON.stringify(item));
  }
}


```
