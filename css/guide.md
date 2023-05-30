# CSS

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
``
a:hover {
}

p::first-line {
}

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
