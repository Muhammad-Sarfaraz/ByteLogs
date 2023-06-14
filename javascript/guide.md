# Hands on Note for Javascript

#### Util:

###### Breadcrum Format [routePate -> Route Path]:
```
// Make pascal to breadcrumb format.
breadcrumbFormat(str) {
return str.replace(/([A-Z])/g, ' $1').trim();
},
```

###### Ucfirst:
```
// Alternative of php's ucfirst.
ucfirst(str) {
      if (typeof str !== 'string' || str.length === 0) {
          return str;
      }

      return str.charAt(0).toUpperCase() + str.slice(1);
},

```


#### The Array Loop Hole:


###### Push:
```
types() {
  const types = [];
  if (Object.keys(this.designationTypes).length > 0) {
    this.designationTypes.forEach(function (type) {
      types.push({
        name: type.name,
        value: type.value,
      });
    });
  }
  return types;
},
```

#### Networking:

###### xhr :
```
const url = 'https://api.example.com/data';
const data = { username: 'JohnDoe', password: 'secretpassword' };

const xhr = new XMLHttpRequest();
xhr.open('POST', url);
xhr.setRequestHeader('Content-Type', 'application/json');

xhr.onload = function() {
  if (xhr.status === 200) {
    const responseData = JSON.parse(xhr.responseText);
    // Handle the response data
    console.log(responseData);
  } else {
    // Handle the error
    console.error('Error:', xhr.status);
  }
};

xhr.onerror = function() {
  // Handle any network errors
  console.error('Network Error');
};

xhr.send(JSON.stringify(data));

```

###### Post:
```
const url = 'https://api.example.com/data';
const data = { username: 'JohnDoe', password: 'secretpassword' };

fetch(url, {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json'
  },
  body: JSON.stringify(data)
})
  .then(response => {
    if (!response.ok) {
      throw new Error('Network response was not ok');
    }
    return response.json();
  })
  .then(responseData => {
    // Handle the response data
    console.log(responseData);
  })
  .catch(error => {
    // Handle any errors that occurred during the request
    console.error('Error:', error);
  });
```

###### Get:
```
fetch('https://api.example.com/data')
  .then(response => {
    if (!response.ok) {
      throw new Error('Network response was not ok');
    }
    return response.json();
  })
  .then(data => {
    // Handle the data received from the server
    console.log(data);
  })
  .catch(error => {
    // Handle any errors that occurred during the request
    console.error('Error:', error);
  });
```
