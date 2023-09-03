# Communication between components [without vueX]

#### Install
```bash
npm i mitt
```

#### Initialize
```js
/*
  The event bus handles the communication between components.
*/

import mitt from 'mitt'
export const EventBus = mitt();

```

#### Use it in Vue

Flow : It basically can emmit a event which can be listen by any ovserer all over the app. First you listen for event ,
execute a push event then the listener will be called each time push is called.


```js

// Import it...
import { EventBus } from "../../../bus.js";

// Set Listener...
 bindEvents() {
  EventBus.on(
    "server",
    function () {
      console.log("Yaay, Server !!!");
    }.bind(this)
  );
},

mounted() {
  this.bindEvents();
},

// Pushser...
```js
 emittOn() {
  EventBus.emit("server");
},
```


