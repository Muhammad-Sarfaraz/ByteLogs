# Hands on Note for Axios

#### Installation:
```npm install axios --save```

#### Axios Interceptors:
You can intercept requests or responses before they are handled by then or catch.
```
import axios from 'axios';

// Create an instance of Axios
const api = axios.create({
  baseURL: 'https://api.example.com',
});

// Request Interceptor
api.interceptors.request.use(
  function (config) {
    // Modify request configuration, add headers, or perform other actions
    console.log('Request Interceptor:', config);
    return config;
  },
  function (error) {
    // Handle request error
    console.error('Request Error:', error);
    return Promise.reject(error);
  }
);

// Response Interceptor
api.interceptors.response.use(
  function (response) {
    // Process response data, handle errors, or make modifications
    console.log('Response Interceptor:', response);
    return response;
  },
  function (error) {
    // Handle response error
    console.error('Response Error:', error);
    return Promise.reject(error);
  }
);

// Make a request
api.get('/users')
  .then(function (response) {
    console.log('Response:', response.data);
  })
  .catch(function (error) {
    console.error('Error:', error);
  });

```

###### Retry:
```
// Create an instance of Axios
const api = axios.create({
  baseURL: 'https://api.example.com',
  // Set the maximum number of retries
  retry: {
    retries: 3
  }
});
```

#### Head:
```
let res = await axios.head('http://google.com');
```

#### Skeleton:
```
axios
          .post('url', {
                name: this.name,
                position: this.position
          })
          .then(response => (console.log(response.data)))
          .catch(error => console.log(error))
          .finally(() => this.loading = false)
```
