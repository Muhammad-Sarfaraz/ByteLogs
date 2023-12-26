# Script

#### Skeleton Content Loading
Show a bare bond skeleton before loading the actual content.
```
npm i vue-content-loader
```

```vue
<template>
  <ContentLoader
    speed="2"
    width="1000"
    height="1000"
    viewBox="0 0 400 160"
    backgroundColor="#f3f3f3"
    foregroundColor="#ecebeb"
  >
    <rect x="48" y="8" rx="3" ry="3" width="88" height="6" />
    <rect x="48" y="26" rx="3" ry="3" width="52" height="6" />
    <rect x="0" y="56" rx="3" ry="3" width="410" height="6" />
    <rect x="0" y="72" rx="3" ry="3" width="380" height="6" />
    <rect x="0" y="88" rx="3" ry="3" width="178" height="6" />
    <circle cx="20" cy="20" r="20" />
  </ContentLoader>

  <button v-debounce-click:1000="onClick">On Click</button>
</template>
<script>
import { ContentLoader } from "vue-content-loader";
export default {
  components: {
    ContentLoader,
  },
}
</script>
```


#### Debounce Button
Prevent user from clicking twice for sometimes.
```html
<button v-debounce-click:1000="onClick">On Click</button>
```
```js
 methods: {
    onClick: function () {
      console.log("Clicked only once");
    },
  },
 directives: {
    "debounce-click": {
      beforeMount(el, binding) {
        const delay = parseInt(binding.arg) || 300;
        let timerId;

        el.addEventListener("click", () => {
          clearTimeout(timerId);
          timerId = setTimeout(() => {
            binding.value();
          }, delay);
        });
      },
    },
  },
```

#### On Change Search
```html
<input type="text" placeholder="Search here" v-model="searchQuery" />
<template v-for="(user, index) in filteredUsers" :key="index">
<li :class="selected_user == user.id ? 'active' : ''">
  <button class="Person" @click.prevent="setSelectedUserAttribute(user.id)">
    <img :src="user?.thumb_two" alt="1" />
    <span>{{ user?.given_name }}</span>
  </button>
</li>
</template>
```
```js
data(){
return{
    users: {},
     searchQuery:"",
    }
},
computed: {
    filteredUsers() {
        const query = this.searchQuery.toLowerCase().trim();
        if (!query) {
          return this.users; // If the query is empty, return all users
        }
        return this.users.filter(user => user.given_name.toLowerCase().includes(query));
    },
},
```

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
- Traditional
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
- Alternative

```compound.js```
```js
export const compound = {
    install(app) {
        app.config.globalProperties.$compound = {
            execute(names) {
                 const data = axios.get('support/get-models', {
                     params: {
                         data: names,
                     }
                 });
                 return data;
            },
        };
    },
};

// Register in app.js.
import {
    compound
} from './plugin/api/compound'
app.use(compound)

// Execute it
this.$compound
  .execute("Member,SessionYear,Division,Designation")
  .then((res) => {
  console.log(res.data)
});

```

