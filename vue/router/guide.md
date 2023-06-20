# Hands on Note for Router

#### Utility:
###### Get current route name:
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

#### Router link:
Note how instead of using regular a tags, we use a custom component router-link to create links.

#### Router view:
router-view will display the component that corresponds to the URL. You can put it anywhere to adapt it to your layout

#### Dynamic router push:

```
this.$router.push({
    path: '/p/' + this.contextMenu.post.id,
    query: { token: this.$route.query.token },
})
```
