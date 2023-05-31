# CSS

#### Height & Width

#### Border:

#### Layout : [Grid,Flex]

#### Selector:

* Type, class, and ID selectors

```
h1 {
}

.box {
}

#unique {
}
```

* Attribute selectors
This group of selectors gives you different ways to select elements based on the presence of a certain attribute on an element:
```
a[title] {
}
a[href="https://example.com"]
{
}
```

* Pseudo-classes and pseudo-elements
```
a:hover {
}

p::first-line {
}
```

article :first-child {
  font-weight: bold;
}
``

* Combinators
The final group of selectors combine other selectors in order to target elements within our documents:
```
article > p {
}
```

#### Center a Image Horizontally and Vertically

HTML:
```
<div class="container">
  <img src="your-image.jpg" alt="Your Image" class="centered-image">
</div>
```
CSS:
```
.container {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh; /* Adjust as needed */
}

.centered-image {
  max-width: 100%;
  max-height: 100%;
}
```
