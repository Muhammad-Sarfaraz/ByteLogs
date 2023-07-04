
# Vue js

#### Short:
Vue: The power of reactive JavaScript for building dynamic user interfaces.

#### What the heck it is?

###### Glimpse of first over-view of vue js app.
- A basic cdn based vue app.
```
<script src="https://unpkg.com/vue@3/dist/vue.global.js"></script>
<div id="app">
  <p>I have a {{ product }}</p>
  <p>{{ product + 's' }}</p>
  <p>{{ isAvailable ? 'YES' : 'NO' }}</p>
</div>

<script>
  const { createApp } = Vue

  createApp({
    data() {
      return {
        product:"Cobra Badminton",
        isAvailable:true,
        message: 'Hello Vue!'
      }
    }
  }).mount('#app')
</script>
```

#### Option API vs Composition API
The Vue.js framework provides two approaches for organizing and managing component logic: the Options API and the Composition API.

* Option API
```
export default {
  data() {
    return {
      message: 'Hello, Vue.js!'
    };
  },
  methods: {
    greet() {
      console.log(this.message);
    }
  }
};
```
- The Options API is the traditional and simpler approach used in earlier versions of Vue.js.
- It involves defining a component using an options object that contains various properties and methods.
- The component options include data, computed, methods, watch, and others, allowing you to structure and manage component behavior.


* Composition API
```
import { reactive, computed, watch } from 'vue';

export default {
  setup() {
    const state = reactive({
      message: 'Hello, Vue.js!'
    });

    const greet = () => {
      console.log(state.message);
    };

    return {
      state,
      greet
    };
  }
};
```
- The Composition API is a newer approach introduced in Vue 3 that provides more flexibility and reusability for managing component logic.
- It allows you to organize code based on logical concerns rather than options objects.
- It involves using functions and reactive utilities to create reusable logic and composition functions.

#### Life Cycle Hooks

```
The total life cycle hooks of vue js given below:
- beforeCreate
- created
- beforeMount
- mounted
- beforeUpdate
- updated
- beforeDestroy
- destroyed
```

##### beforeCreate:
The beforeCreate hook runs at the very initialization of your component. data has not been made reactive, and events have not been set up yet.

Usage
Using the beforeCreate hook is useful when you need some sort of logic/API call that does not need to be assigned to data. Because if we were to assign something to data now, it would be lost once the state was initialized.

##### created:
You are able to access reactive data and events that are active with the created hook. Templates and Virtual DOM have not yet been mounted or rendered.

Usage
Using the created method is useful when dealing with reading/writing the reactive data. For example, if you want to make an API call and then store that value, this is the place to do it.
The above are famously called as creation hooks, as opposed to mounting hooks.
Mounting hooks are often the most used hooks. They allow you to access your component immediately before and after the first render. They do not, however, run during server-side rendering.

##### beforeMount:
The beforeMount hook runs right before the initial render happens and after the template or render functions have been compiled.

Usage
This is the last step you should perform your API calls before it’s unnecessary late in the process because it’s right after created — they have access to the same component variables.

##### mounted:
In the mounted hook, you will have full access to the reactive component, templates, and rendered DOM (via this.$el).

Usage
Use mounted for modifying the DOM—particularly when integrating non-Vue libraries.

There also some hooks, which are called updating hooks.

Updating hooks are called whenever a reactive property used by your component changes or something else causes it to re-render. They allow you to hook into the watch-compute-render cycle for your component.

Use updating hooks if you need to know when your component re-renders, perhaps for debugging or profiling.

There are:

##### beforeUpdate:
The beforeUpdate hook runs after data changes on your component and the update cycle begins, right before the DOM is patched and re-rendered.

Usage
Use beforeUpdate if you need to get the new state of any reactive data on your component before it actually gets rendered.

##### updated:
The updated hook runs after data changes on your component and the DOM re-renders.

Usage
Use updated if you need to access the DOM after a property change

And last but not least, there are destruction hooks.

Destruction hooks allow you to perform actions when your component is destroyed, such as cleanup or analytics sending. They fire when your component is being torn down and removed from the DOM.

There are:

##### beforeDestroy:
beforeDestroy is fired right before teardown. Your component will still be fully present and functional.

Usage
Use beforeDestroy if you need to clean-up events or reactive subscriptions.

This is the stage where you can do resource management, delete variables and clean up the component.

##### destroyed:
By the time you reach the destroyed hook, there’s practically nothing left on your component. Everything that was attached to it has been destroyed.

Usage
Use destroyed if you need do any last-minute cleanup or inform a remote server that the component was destroyed

#### Template Refs
In Vue.js, when you're building a web page, you can think of it as a big box full of different things, just like your toy box. Sometimes, you want to interact with a specific part of the web page, like a button or a picture. That's where template refs come in!

```
<div id="app">
  <h1>Counter: {{ counter }}</h1>
  <button @click="increment">Increment</button>
  <button @click="decrement">Decrement</button>
  <button ref="resetButton" @click="reset">Reset</button> <!-- Use case of Template ref -->
</div>

new Vue({
  el: '#app',
  data: {
    counter: 0
  },
  methods: {
    increment() {
      this.counter++;
    },
    decrement() {
      this.counter--;
    },
    reset() {
      this.counter = 0;
      this.$refs.resetButton.disabled = true; // Use case of Template ref
    }
  }
});
```

#### Data:
```
  data: () => ({
    order: JSON.parse(localStorage.getItem(STORAGE_KEY) || '[]'),
  }),
```


#### Components
A component in Vue.js is a modular and reusable building block that encapsulates the logic, template, and styling of a specific part of a web application, promoting code organization and reusability.

// In Child
```
<template>
  <div>
    <h2>Welcome to the Playroom!</h2>
    <button @click="play">Play with Toys</button>
  </div>
</template>

<script>
export default {
  methods: {
    play() {
      alert('Having fun playing with toys!');
    }
  }
}
</script>

<style scoped>
h2 {
  color: blue;
}
</style>

```
// In parent
```
<template>
  <div>
    <h1>Welcome to the Music room!</h1>
    <playroom></playroom>
  </div>
</template>

<script>
import Playroom from './Playroom.vue';

export default {
  components: {
    Playroom
  }
}
</script>
```

##### Data passing from between child and parent.

// Parent
```
<template>
  <div>
    <h2>ParentToy</h2>
    <button @click="passCarToChild">Pass Car to Child</button>
    <ChildToy :car="car" @toyReceived="handleToyReceived"></ChildToy>
  </div>
</template>

<script>
import ChildToy from './ChildToy.vue';

export default {
  components: {
    ChildToy
  },
  data() {
    return {
      car: 'Toy Car'
    };
  },
  methods: {
    passCarToChild() {
      this.car = ''; // Empty the car
    },
    handleToyReceived() {
      alert('ChildToy received the car!');
    }
  }
}
</script>
```

#### Async Component

Example of async componet:

Child Component:
```
<template>
  <div>
    <h2>{{ message }}</h2>
    <p>Loading...</p>
  </div>
</template>

<script>
export default {
  data() {
    return {
      message: ''
    };
  },
  async created() {
    // Simulating an asynchronous operation
    await new Promise(resolve => setTimeout(resolve, 2000));
    this.message = 'Async component loaded!';
  }
};
</script>
```

Root Component:
```
<template>
  <div>
    <async-component></async-component>
  </div>
</template>

<script>
import { defineAsyncComponent } from 'vue';

const AsyncComponent = defineAsyncComponent(() =>
  import('./AsyncComponent.vue')
);

export default {
  components: {
    AsyncComponent
  }
};
</script>
```

#### Provide / Inject
The provide and inject options in Vue.js allow you to share data or methods between components in a parent-child relationship without explicitly passing props

Parent:
```
<template>
  <div>
    <child-component></child-component>
  </div>
</template>

<script>
import { provide } from 'vue';
import ChildComponent from './ChildComponent.vue';

export default {
  components: {
    ChildComponent
  },
  data() {
    return {
      message: 'Hello from the parent component!'
    };
  },
  provide() {
    return {
      sharedMessage: this.message
    };
  }
};
</script>

```

Child:
```
<template>
  <div>
    <p>{{ sharedMessage }}</p>
  </div>
</template>

<script>
import { inject } from 'vue';

export default {
  setup() {
    const sharedMessage = inject('sharedMessage');

    return {
      sharedMessage
    };
  }
};
</script>

```

#### Slot
 A slot in Vue.js is like a place where you can put different puzzle pieces to complete a picture.
 You can write style in slot indiviually but affect will show on the child. More, please see the [AuraVue]

Root Component: [Content]
```
<template>
  <div>
    <Exam>
      <template v-slot:ct>
        <Item name="Bangla"></Item>
        <Item name="English"></Item>
      </template>
      <template v-slot:mid>
         <Item name="Bangla"></Item>
        <Item name="English"></Item>
      </template>
      <template v-slot:final>
        <Item name="Bangla"></Item>
        <Item name="English"></Item>
      </template>
    </Exam>
  </div>
</template>

<script>
import Exam from './Exam.vue';
import Item from './Item.vue';

export default {
  components: {
    Board,
    Item
  }
};
</script>
```
Exam Component: [Master Layout]
```
<template>
  <div>
    <h1>Welcome to the Board!</h1>
    <slot name="ct"></slot> <!-- This is the slot for CT -->
    <slot name="mid"></slot> <!-- This is the slot for Mid -->
    <slot name="final"></slot> <!-- This is the slot for Final -->
  </div>
</template>

```
Item Component:
```
<template>
  <div>
    <h2>{{ name }}</h2>
  </div>
</template>

<script>
export default {
  props: {
    name: String
  }
};
</script>
```

Child Component:
```
<template>
  <div>
    <h3>ChildToy</h3>
    <p>Received Toy: {{ receivedToy }}</p>
    <button @click="sendEventToParent">Send Event to Parent</button>
  </div>
</template>

<script>
export default {
  props: ['car'],
  data() {
    return {
      receivedToy: ''
    };
  },
  methods: {
    sendEventToParent() {
      this.$emit('toyReceived');
      this.receivedToy = this.car; // Receive the toy car
    }
  }
}
</script>

```

#### Watchers
Watch on reactive property changes: It will run whenever the reactive property of cart changes.

```
data(){
    return{
        cart:[],
    }
},

 watch: {
    cart(current, old) {
      if (Object.keys(current).length > 0) {
        this.getDiscount()
      }
    }
  },
```


#### Directives

```
<p v-if="inStock">{{ product }}</p>
<p v-else-if="onSale">...</p>
<p v-else>...</p>
```


```
<p v-show="showProductDetails">...</p>
```

#### Data binding

```
<input v-model="firstName">
v.model.lazy="..." // Syncs input after change event
v.model.number="..." // Always returns a number
v.model.trim="..." // Strips whitespace
```

#### List rendering

```
<li v-for="item in items" :key="item.id">
  {{ item }}
</li>
```

* Access position
```
<li v-for="(item, index) in items">...</li>
```

* Iterate 

```
<li v-for="value in object">...</li>
<li v-for="(value, index) in object">...</li>
<li v-for="(value, name, index) in object">...</li>
```

* In component

```
<cart-product v-for="item in products" :product="item" :key="item.id">
```

* Binding

```
<a v-bind:href="url">...</a>
<a :href="url">...</a> // Shorthand
```

#### Actions/Events

```
<button v-on:click="addToCart">...</button>
<button @click="addToCart">...</button> // Shorthand
<button @click="addToCart(product)">...</button>
<form @submit.prevent="addProduct">...</form>

```

#### Network

* Fetch data using javascript fetch

```
<template>
  <div>
    <button @click="fetchData">Fetch Data</button>
    <ul v-if="data">
      <li v-for="item in data" :key="item.id">{{ item.name }}</li>
    </ul>
  </div>
</template>

<script>
export default {
  data() {
    return {
      data: null
    };
  },
  methods: {
    fetchData() {
      fetch('https://api.example.com/data') // Replace with your API endpoint
        .then(response => response.json())
        .then(data => {
          this.data = data;
        })
        .catch(error => {
          console.error('Error fetching data:', error);
        });
    }
  }
};
</script>
```

* Post data using javascript fetch
```
<template>
  <div>
    <button @click="postData">Post Data</button>
  </div>
</template>

<script>
export default {
  methods: {
    postData() {
      const data = {
        name: 'John',
        age: 25
      };

      fetch('https://api.example.com/data', {
        method: 'POST',
        headers: {
          'Content-Type': 'application/json'
        },
        body: JSON.stringify(data)
      })
        .then(response => response.json())
        .then(data => {
          console.log('Data posted successfully:', data);
        })
        .catch(error => {
          console.error('Error posting data:', error);
        });
    }
  }
};
</script>
```

* Fetch data using axios

```
<template>
  <div>
    <button @click="fetchData">Fetch Data</button>
    <ul v-if="data">
      <li v-for="item in data" :key="item.id">{{ item.name }}</li>
    </ul>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      data: null
    };
  },
  methods: {
    fetchData() {
      axios.get('https://api.example.com/data') // Replace with your API endpoint
        .then(response => {
          this.data = response.data;
        })
        .catch(error => {
          console.error('Error fetching data:', error);
        });
    }
  }
};
</script>
```

* Post data using axios

```
<template>
  <div>
    <button @click="postData">Post Data</button>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  methods: {
    postData() {
      const data = {
        name: 'John',
        age: 25
      };

      axios.post('https://api.example.com/data', data) // Replace with your API endpoint
        .then(response => {
          console.log('Data posted successfully:', response.data);
        })
        .catch(error => {
          console.error('Error posting data:', error);
        });
    }
  }
};
</script>

```

#### Form Data
FormData is a JavaScript object used to collect and manage form data for easy submission.

* Using the data property:
  - You store the form data directly in the component's data property as separate variables or objects.
  - You can easily access, manipulate, and validate the form data within the component's methods.
  - This approach gives you full control over the form data and allows you to customize its handling according to your needs.

* Using FormData:

- FormData is a built-in JavaScript object specifically designed to handle form data.
- It provides a convenient way to collect form field values and construct a payload for sending as a request.
- FormData is useful when dealing with more complex forms, such as those with file uploads or when you need to send data in a specific format.
- It simplifies the process of handling and sending form data, especially in scenarios where the form structure or data requirements are more specialized.

* Submit form without axios/ajax

```
<template>
  <div>
    <form @submit="submitForm">
      <label for="name">Name:</label>
      <input type="text" id="name" v-model="formData.name" required>
      <br>
      <label for="age">Age:</label>
      <input type="number" id="age" v-model="formData.age" required>
      <br>
      <button type="submit">Submit</button>
    </form>
    <div v-if="submitted">
      <h3>Submitted Data:</h3>
      <p>Name: {{ submittedData.name }}</p>
      <p>Age: {{ submittedData.age }}</p>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      formData: {
        name: '',
        age: null
      },
      submitted: false,
      submittedData: {}
    };
  },
  methods: {
    submitForm(event) {
      event.preventDefault(); // Prevent the default form submission behavior

      // Perform any validation or data manipulation here if needed

      // Store the submitted data
      this.submittedData = {
        name: this.formData.name,
        age: this.formData.age
      };

      this.submitted = true;
    }
  }
};
</script>

```

* Using axios

```
<template>
  <div>
    <form @submit="submitForm">
      <label for="name">Name:</label>
      <input type="text" id="name" v-model="formData.name" required>
      <br>
      <label for="age">Age:</label>
      <input type="number" id="age" v-model="formData.age" required>
      <br>
      <button type="submit">Submit</button>
    </form>
    <div v-if="submitted">
      <h3>Submitted Data:</h3>
      <p>Name: {{ submittedData.name }}</p>
      <p>Age: {{ submittedData.age }}</p>
    </div>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      formData: {
        name: '',
        age: null
      },
      submitted: false,
      submittedData: {}
    };
  },
  methods: {
    submitForm(event) {
      event.preventDefault(); // Prevent the default form submission behavior

      const formData = new FormData();
      formData.append('name', this.formData.name);
      formData.append('age', this.formData.age);

      axios.post('https://api.example.com/submit', formData)
        .then(response => {
          this.submittedData = response.data;
          this.submitted = true;
        })
        .catch(error => {
          console.error('Error submitting form:', error);
        });
    }
  }
};
</script>

```

#### Vue Router

* A simple example

```
<script>
import Home from './Home.vue'
import About from './About.vue'
import NotFound from './NotFound.vue'

const routes = {
  '/': Home,
  '/about': About
}

export default {
  data() {
    return {
      currentPath: window.location.hash
    }
  },
  computed: {
    currentView() {
      return routes[this.currentPath.slice(1) || '/'] || NotFound
    }
  },
  mounted() {
    window.addEventListener('hashchange', () => {
		  this.currentPath = window.location.hash
		})
  }
}
</script>

<template>
  <a href="#/">Home</a> |
  <a href="#/about">About</a> |
  <a href="#/non-existent-path">Broken Link</a>
  <component :is="currentView" />
</template>
```

* Scroll behaviour

```
const router = createRouter({
  history: createWebHistory(),
  routes,
  scrollBehavior(to, from, savedPosition) {
    if (savedPosition) {
      return savedPosition;
    } else {
      return { top: 0 };
    }
  }
});

```

* On Error

```
router.onError(error => {
  // Handle the error
});
```

* History mode
```
const router = createRouter({
  history: createWebHistory(),
  routes
});

```

* Go to a specific page

```
export default {
  methods: {
    goToAboutPage() {
      this.$router.push('/about');
    }
  }
}
```

* Navigation

```
<router-link to="/">Home</router-link>
<router-link to="/about">About</router-link>
```

* Nested route

```
const routes = [
  {
    path: '/users',
    component: Users,
    children: [
      { path: '', component: UsersList },
      { path: ':id', component: UserDetails }
    ]
  }
];
```

* Router view

```
<template>
  <div id="app">
    <router-view></router-view>
  </div>
</template>
```

* Route Navigation Guards:
There are several types of guards available, such as beforeEach, beforeEnter, beforeLeave, beforeRouteUpdate, and more.
```
router.beforeEach((to, from, next) => {
  // Perform some logic before navigating to the next route
  if (to.meta.requiresAuth && !isLoggedIn) {
    next('/login');
  } else {
    next();
  }
});
```

## VueX
Vuex is a state management library for Vue.js that helps manage the application state in a centralized manner, providing easy access and modification of state across components.
A simple overview given below,

Key Concepts in Vuex:

- State: The single source of truth for the application's data.
- Mutations: Functions that modify the state synchronously.
- Actions: Functions that can perform asynchronous operations and commit mutations.
- Getters: Computed properties that derive values from the state.

* Accessing the State:
- Use $store.state to access the state in your components.
- Example: ``` this.$store.state.counter ```

* Committing Mutations:
- Mutations are functions that modify the state.
- Use commit to invoke mutations.
- Example: ``` this.$store.commit('increment') ```

* Dispatching Actions:
- Actions are functions that can perform asynchronous operations and commit mutations.
- Use dispatch to invoke actions.
- Example: ``` this.$store.dispatch('fetchData') ```

* Using Getters:

- Getters are computed properties based on the state.
- Access getters using $store.getters.
- Example: ``` this.$store.getters.getFormattedData ```

store.js
```
import { createStore } from 'vuex';

const store = createStore({
  state: {
    counter: 0
  },
  mutations: {
    increment(state) {
      state.counter++;
    },
    decrement(state) {
      state.counter--;
    }
  },
  actions: {
    increment(context) {
      context.commit('increment');
    },
    decrement(context) {
      context.commit('decrement');
    }
  },
  getters: {
    counter(state) {
      return state.counter;
    }
  }
});

export default store;
```

Registration
```
import { createApp } from 'vue';
import App from './App.vue';
import store from './store';

const app = createApp(App);
app.use(store);
app.mount('#app');
```

Accessing the Store in Components:
```
<template>
  <div>
    <p>Counter: {{ counter }}</p>
    <button @click="increment">Increment</button>
    <button @click="decrement">Decrement</button>
  </div>
</template>

<script>
export default {
  computed: {
    counter() {
      return this.$store.getters.counter;
    }
  },
  methods: {
    increment() {
      this.$store.dispatch('increment');
    },
    decrement() {
      this.$store.dispatch('decrement');
    }
  }
};
</script>
```

#### Advance Topic:
###### Custom Directives
###### Composables
###### Plugins
Plugins are self-contained code that usually add app-level functionality to Vue.

* Step 01 :  create it:
```
export const world = {
    install(app) {
      app.config.globalProperties.$world = {
        execute() {
          return "Hello World!"; 
        },
      };
    },
  };
```
* Step 02 : Register it:
```
const app = createApp(App)
app.use(world);
```

* Execute it:
 ```
this.$world.execute()
  ```
