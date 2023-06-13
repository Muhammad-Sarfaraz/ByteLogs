# Hands on Note for Javascript

#### Networking:

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
