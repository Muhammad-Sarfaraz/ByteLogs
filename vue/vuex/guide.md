# Hands on Note for Vuex

#### Magic method:
```
$store
```

#### Skeleton:
```
import Vue from 'vue'
import Vuex from 'vuex'

Vue.use(Vuex)

export default new Vuex.Store({
  state: {
    
  },
  getters: {
  },
  mutations: {
  },
  actions: {
  },
  modules: {
  }
})
```

#### Use state in component:
```
<li v-for="(list, index) in $store.state.lists" :key="index">
            <a href="#">
                {{ list.name }}
            </a>
        </li>
```

#### Update state:
* Using functionality stand point:
```
$store.state.select = list.id;
```

* Using Mutation and Commit:
```
// Inside the store:
state: {
  select:-1;
},
mutations: {
    select(state,payload){
      state.select = payload;
    }
  },

// Call it from the template:
<button @click.prevent="$store.commit('select',list.id);"></button>
```

#### Getters aka [Computed Property] : 
Getter are like computed property, which is built in vux.

```
// Inside component:
 <p v-for="(item,index) in $store.getters.selectedIltems" :key="index">
            {{ item.text }}
        </p>
        
// Inside store:
 getters: {
    selectedIltems(state){
      let list = state.lists.find(l => l.id === state.select);
      console.log(list)
      if(list){
          return list.items;
      }
      return [];
     }
  },
```

#### Mutation Vs Action
* Mutation : 
  - Do not do async in mutation.
  - Mutation directly mutate our state
* Action:
   - Action can do async job.
   - we can commit a mutation from action.

* Step:
  - Define the action.
  - call the mutator by commiting.
  - update the state from mutator
  - Flow [dispatch->action->mutator->state]

```
actions:{
init({context}){
  fetch(http:localhost:3000/lists).the((res)=> res.json()).then(lists => {
    commit('loadLists',lists);
  }
}
}

// Now dispatch the action
store.dispatch('init');

// of Inside component to dispatch the action:
created() {
      this.$store.dispatch('init')
    },

```

#### Create Logger:
```
import Vuex from 'vuex'
```

#### Dynamic class:
```
:class="{active: $store.state.select == list.id}"
```










