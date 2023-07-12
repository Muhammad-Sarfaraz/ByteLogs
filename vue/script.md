# Script

####  Manually Active Link:
```

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

```
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

```
this.$scroll.execute('scrollToDivId')
```

#### The Compound Data Object:

Suppose, You have to get data of 3/4 models, what will you do ? you will call one by one , but cost time and resources. Instead just 
make a single api call and get all the data which you are looking for!

```
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
