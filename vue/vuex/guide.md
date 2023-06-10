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

#### Map:
Map in vuex are like alias, there is some alias for getters,state and mutations.

**Import** ``` import {mapState,mapMutations,mapGetters} from 'vuex' ```

###### Map State:
```

// Inside the store vuex:
 state: {
    mapState:"Yes, this is a mapState",
}
// Inside the computed property:
 computed:{
 ...mapState([
            'mapState' // Name of the state in the Vuex,
        ]),
 }
 
 // Call it in the template:
 // Before: $store.state.mapState
 // After : mapState
<h3>Map State : {{ mapState }}</h3>

// For Custom named state:
...mapState({
      customState: 'mapState'
    })
<h3>Map State : {{ customState }}</h3>
```

#### Map Mutations
```
// Inside the methods.
methods: {
        foo(){
            alert('All Ok!');
        },
        ...mapMutations([
            'action'
        ])
    },
    
// Custom named mutations:
...mapMutations({
      customAction: 'action'
    })
    
// Inside the template:
<button @click="action('Execute')" >Fire Action</button>     

// Before: 
<button @click="$store.commit('action','Execute')" >Fire Action</button>  
// After: 
<button @click="action('Execute')" >Fire Action</button>     
```

#### Map Getters:
```
// Inside the computed property:
 computed:{
        ...mapGetters([
            'mapGetters' // Name o f your getter
        ])
    },
    
// Inside the template:
 <h3>Map Getters : {{ mapGetters }}</h3>
 
 // Custom named getter:
  ...mapGetters({
      customGetter: 'mapGetters' // Name of your getter
    })
```

#### Create Logger:
```
import Vuex from 'vuex'
```

#### Dynamic class:
```
:class="{active: $store.state.select == list.id}"
```










