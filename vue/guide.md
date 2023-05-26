# What the heck it is?

* Glimpse of first view.
- A basic cdn based vue app.
```<script src="https://unpkg.com/vue@3/dist/vue.global.js"></script>

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
</script>```

* Life Cycle Hooks

```
beforeCreate
created
beforeMount
mounted
beforeUpdate
updated
beforeDestroy
destroyed


beforeCreate
The beforeCreate hook runs at the very initialization of your component. data has not been made reactive, and events have not been set up yet.

Usage
Using the beforeCreate hook is useful when you need some sort of logic/API call that does not need to be assigned to data. Because if we were to assign something to data now, it would be lost once the state was initialized.

created
You are able to access reactive data and events that are active with the created hook. Templates and Virtual DOM have not yet been mounted or rendered.

Usage
Using the created method is useful when dealing with reading/writing the reactive data. For example, if you want to make an API call and then store that value, this is the place to do it.

The above are famously called as creation hooks, as opposed to mounting hooks.

Mounting hooks are often the most used hooks. They allow you to access your component immediately before and after the first render. They do not, however, run during server-side rendering.

beforeMount
The beforeMount hook runs right before the initial render happens and after the template or render functions have been compiled.

Usage
This is the last step you should perform your API calls before it’s unnecessary late in the process because it’s right after created — they have access to the same component variables.

mounted
In the mounted hook, you will have full access to the reactive component, templates, and rendered DOM (via this.$el).

Usage
Use mounted for modifying the DOM—particularly when integrating non-Vue libraries.

There also some hooks, which are called updating hooks.

Updating hooks are called whenever a reactive property used by your component changes or something else causes it to re-render. They allow you to hook into the watch-compute-render cycle for your component.

Use updating hooks if you need to know when your component re-renders, perhaps for debugging or profiling.

There are:

beforeUpdate
The beforeUpdate hook runs after data changes on your component and the update cycle begins, right before the DOM is patched and re-rendered.

Usage
Use beforeUpdate if you need to get the new state of any reactive data on your component before it actually gets rendered.

updated
The updated hook runs after data changes on your component and the DOM re-renders.

Usage
Use updated if you need to access the DOM after a property change

And last but not least, there are destruction hooks.

Destruction hooks allow you to perform actions when your component is destroyed, such as cleanup or analytics sending. They fire when your component is being torn down and removed from the DOM.

There are:

destroyed
By the time you reach the destroyed hook, there’s practically nothing left on your component. Everything that was attached to it has been destroyed.

Usage
Use destroyed if you need do any last-minute cleanup or inform a remote server that the component was destroyed

beforeDestroy
beforeDestroy is fired right before teardown. Your component will still be fully present and functional.

Usage
Use beforeDestroy if you need to clean-up events or reactive subscriptions.

This is the stage where you can do resource management, delete variables and clean up the component.



* Template Refs
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


``

* Components

````

// In Child
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

// In parent
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

* Data passing from between child and parent.

```
// Parent

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



```
// Child

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



* Watchers
Watch on reactive property changes:
It will run whenever the reactive property of cart changes.

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


* Directives

```
<p v-if="inStock">{{ product }}</p>
<p v-else-if="onSale">...</p>
<p v-else>...</p>
```


```
<p v-show="showProductDetails">
  ...
</p>

```

* Data binding

```
<input v-model="firstName">
v.model.lazy="..." // Syncs input after change event
v.model.number="..." // Always returns a number
v.model.trim="..." // Strips whitespace
```

* List rendering

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

* Actions/Events

```
<button v-on:click="addToCart">...</button>
<button @click="addToCart">...</button> // Shorthand
<button @click="addToCart(product)">...</button>
<form @submit.prevent="addProduct">...</form>

```