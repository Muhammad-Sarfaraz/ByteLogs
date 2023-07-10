# Hands on Note for Router

#### Alias
An alias of / as /home means when the user visits /home, the URL remains /home, but it will be matched as if the user is visiting /
```
const routes = [{ path: '/', component: Homepage, alias: '/home' }]
```

#### Named Views
Sometimes you need to display multiple views at the same time instead of nesting them
```
<router-view class="view left-sidebar" name="LeftSidebar"></router-view>
<router-view class="view main-content"></router-view>
<router-view class="view right-sidebar" name="RightSidebar"></router-view>
```

#### Utility:

#### hasRoute:
Checks if a route with a given name exists
```
router.hasRoute(ROUTE_NAME);
```


Push to a url, route-name

###### Get Current Route Name:
```
{{ currentRouteName }}

computed: {
  currentRouteName() {
    return this.$route.name;
  },
},
```

#### Installation:
``` npm install vue-router@4 ```

#### Setup:
``` main.js ```
```
import Vue from 'vue'
import App from './App.vue'
import router from './router'
import store from './store'

Vue.config.productionTip = false

new Vue({
  router,
  store,
  render: h => h(App)
}).$mount('#app')
```

``` router/index.js ```
```
import Vue from 'vue'
import VueRouter from 'vue-router'
import HomeView from '../views/HomeView.vue'

Vue.use(VueRouter)

const routes = [
  {
    path: '/',
    name: 'home',
    component: HomeView
  },
  {
    path: '/about',
    name: 'about',
    component: () => import(/* webpackChunkName: "about" */ '../views/AboutView.vue')
  }
]

const router = new VueRouter({
  mode: 'history',
  base: process.env.BASE_URL,
  routes
})

export default router

```

#### Router Link:
Note how instead of using regular a tags, we use a custom component router-link to create links.

#### Router view:
router-view will display the component that corresponds to the URL. You can put it anywhere to adapt it to your layout

#### Dynamic Router Push:

```
this.$router.push({
    path: '/p/' + this.contextMenu.post.id,
    query: { token: this.$route.query.token },
})
```
