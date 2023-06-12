# Hands on Note for Axios

#### Installation:
```npm install axios --save```

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
