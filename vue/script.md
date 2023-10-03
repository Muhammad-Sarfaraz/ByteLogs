# Script

#### Same File Doesn't Select after Closing

You have to clear the input, that's the solutions.

```html
<input class="d-none" type="file" id="file" accept=".doc,.docx,.pdf"
    ref="file_uploader" @click="resetFileUploader" @change="onFileChange" />
```
```js
onFileChange(e) {
   const file = e.target.files[0];
   this.data.file_path = file;
   this.data.file_name = file.name;
},
resetFileUploader() {
  this.$refs.file_uploader.value = '';
},
clearFile() {
   this.data.file_path = "";
   this.data.file_name = "";
},
```

#### Is Last Index
```js
isLastItem(data, index) {
   if (data) {
     if (Array.isArray(data)) {
       return index === data.length - 1;
     } else if (typeof data === "object") {
       const keys = Object.keys(data);
       return index === keys.length - 1;
     }
   }
   return false;
},
```

#### Current Date:
```js
date: new Date().toLocaleDateString("en-GB").split("/").join("-"), // 10-08-2023
```

#### Multiple Async Request:
```javascript
async submit() {
   const request1 = '...';
   const request2 = '...';
   const response1 = await fetch(request1).then(response => response.data)
   const response2 = await fetch(request2).then(response => response.data)
}
```

####  Manually Active Link:
```javascript
<router-link>:class="
currentActiveRoute == root_menu.route_name
  ? 'router-link-active active'
  : ''
"</router-link>

data() {
return {
  currentActiveRoute: "",
};
},

watch: {
    $route(newRoute, lastRoute) {
      this.isActiveRoute(this.currentRouteName);
    },
  },
// Methods
methods:{
isActiveRoute(routeName) {
  const parts = routeName.split(".");
  let extractedName = parts[0];
  const makeActivableRoute = (extractedName += ".index");

  const element = document.querySelector(
    `[data-route="${makeActivableRoute}"]`
  );

  if (element) {
    this.currentActiveRoute = makeActivableRoute;
  }
},
}
```

#### Global Scroll:

* First, create the plugin:

```javascript
export const scroll = {
    install(app) {
        app.config.globalProperties.$scroll = {
            execute(selector) {
                var container = document.querySelector(`#${selector}`);
                console.log(container);
                if (container) {
                    container.scrollIntoView({
                        behavior: 'smooth'
                    });
                }
            },
        };
    },
};

```

* Register in vue global, then

```javascript
this.$scroll.execute('scrollToDivId')
```

#### The Compound Data Object:

Suppose, You have to get data of 3/4 models, what will you do ? you will call one by one , but cost time and resources. Instead just 
make a single api call and get all the data which you are looking for!

```php
// Laravel backend:
Route::get('support/get-models', function (Request $request) {
  $data = [];

  if ($request->has('data')) {
      $modelNames = $request->get('data');
      $modelNamesArray = explode(',', $modelNames);

      foreach ($modelNamesArray as $modelName) {
          $model = app("App\Models\\" . ucfirst($modelName));
          $modelData = $model->all();
          $data[$modelName] = $modelData;
      }
  }
  return response()->json($data);
});

```
```js
// In crud.js
getModelsData(names){
  const data = axios.get('support/get-models',{
      params:{
          data:names,
      }
  });
  return data;
},

// Where it is required!
created(){
this.getModelsData("Event,Calendar").then((res)=>{
    console.log(res.data);
});
}

```
