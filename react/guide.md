# A Hands-On Guide to React

#### useDefferedValue
```
const deferredValue = useDeferredValue(value)
```


#### Generating Ids
```
const id = useId()
```


#### Use Effect Hook
 

```
(() => {
    const connection = createConnection(roomId);
    connection.connect();
    return () => connection.disconnect();
  }, [
]);
```




#### State Hook

```
const [index, setIndex] = useState(0);
```

#### A File Attach
```
return (
  <img
    className="avatar"
    src={user.imageUrl}
  />
);
```

#### CRUD:
- Delete
```
deleteNote = async note => {
  const input = { id: note.id }
  const notes = this.state.notes.filter(n => n.id !== note.id)
  this.setState({ notes })
  try {
    await API.graphql(graphqlOperation(deleteNote, { input }))
  } catch (err) {
    console.log('error deleting note...', err)
  }
}
```

#### Webhook:

#### Networking:

#### Event:

```
<button onClick={fire}>Fire!</button>

```

```


<button onClick={fire}>Fire!</button>

```
