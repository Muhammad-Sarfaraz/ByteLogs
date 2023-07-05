# Script:


###### Slice a array into N:
```

```



```
const score = function(){
    return 100;
}

let names = [
    {name:"Hasan",title:"hasan",count:[10,20,30]},
    {name:"Abdul",title:"hasan",count:[50,80,30]},
    {name:"Karim",title:"hasan",count:[20,20,90]}
]

let surnames = {
    name:['khan','rahman','haque']
};

// Sum up all the count:
const sumOfFirstIndex = names[0].count.reduce((oldValue,newValue) => oldValue+newValue);
console.log("Sum of first index :",sumOfFirstIndex);

let totalSum = 0;
names.forEach((obj) => {
  totalSum += obj.count.reduce((accumulator, currentValue) => accumulator + currentValue, 0);
});
console.log("Total sum of count:", totalSum);

// Replace all with their total sum:
let modifiedNames = JSON.parse(JSON.stringify(names)); // Create a deep copy of the names array

modifiedNames.forEach((obj) => {
  const totalSum = obj.count.reduce((accumulator, currentValue) => accumulator + currentValue, 0);
  obj.count = totalSum;
});

console.log("Replace all with their total sum:", modifiedNames);

// Type 01:
console.log(names[0].count[0]);

// Type 02:
names[0].count.map((data)=>{
    console.log(data);
})

// Type 03:
names.map((data)=>{
    console.log("Name :",data.name,"Title :",data.title);
    console.log("Count of name:")
    data.count.map((data)=>{
        console.log(data);
    })
})

// Filter out the data with name "Karim":
const withoutKarim = names.filter((res)=>{
    return res.name !== 'Karim'
});

console.log("Without Karim :");
console.log(withoutKarim);

// Find name "Abdul" and delete it:
// Hint: Find the index , then use splice

const indexOfAbdul = names.findIndex((obj)=>{
   return obj.name === "Abdul";
});


console.log("Index of Abdul is:",indexOfAbdul);
names.splice(indexOfAbdul,1);
console.log("After deletion:",names);

// Best practice:
if (indexOfAbdul !== -1) {
    names.splice(indexOfAbdul, 1);
}

let array = [
    { id: 1, name: 'Hasan' },
    { id: 2, name: 'Abdul' },
    { id: 3, name: 'Karim' },
  ];

  const specificId = 1;
  let filter = array.filter(item => item.id === specificId);
  
  console.log(filter);

export default score;
```
