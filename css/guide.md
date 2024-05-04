# Note on CSS

#### Layout:
- Normal flow
- The display property
- Flexbox
- Grid
- Floats
- Positioning
- Table layout
- Multiple-column layout

#### The !important Rule:
!important rule, it will override ALL previous styling rules for that specific property on that element!

#### Box Model:

#### Height & Width:

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
# Absulate vs Relative
- Absolute positioning: It's like sticking a sticker on a moving object, it stays where you put it. (bsolute" (abs), it stays fixed where you put it)
Element will be positioned relative to the ancestor.

- Relative positioning: It's like moving a toy block from its original spot, but it still knows where it came from. (you can move it from where it would normally be)
Element will be positioned relative to it's original position.

```html

<style>
.container {
  position: relative;
  height: 200px;
  width: 200px;
  border: 2px solid black;
}
.box {
  width: 50px;
  height: 50px;
  background-color: lightblue;
  border: 1px solid blue;
}
.abs {
  position: absolute;
  top: 20px;
  left: 20px;
}

.rel {
  position: relative;
  top: 20px;
  left: 20px;
}
</style>
<div class="container">
  <div class="box abs">Absolute</div>
  <div class="box rel">Relative</div>
</div>


```


# Margin vs Padding

- Padding: Use it when you want space inside the box, around the content.
```csss
padding: top right bottom left;
padding: 10px; /* Applies 10px padding to all sides */
padding: 10px 20px; /* Applies 10px padding to top and bottom, and 20px padding to right and left */
padding: 10px 20px 15px; /* Applies 10px padding to top, 20px padding to right and left, and 15px padding to bottom */
padding: 10px 20px 15px 5px; /* Applies 10px padding to top, 20px padding to right, 15px padding to bottom, and 5px padding to left */
```

- Margin: Use it when you want space outside the box, around the element.


```css
margin: top right bottom left;
margin: 10px; /* Applies 10px margin to all sides */
margin: 10px 20px; /* Applies 10px margin to top and bottom, and 20px margin to right and left */
margin: 10px 20px 15px; /* Applies 10px margin to top, 20px margin to right and left, and 15px margin to bottom */
margin: 10px 20px 15px 5px; /* Applies 10px margin to top, 20px margin to right, 15px margin to bottom, and 5px margin to left */

```

# Layout
- Box Model:
Basic layout method for simple spacing and sizing.

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Box Model</title>
  <style>
    .box {
      width: 200px;
      height: 100px;
      padding: 20px;
      border: 2px solid black;
      margin: 20px;
    }
  </style>
</head>
<body>
  <div class="box">Box Model</div>
</body>
</html>

```

- Table Layout: Primarily for tabular data, not recommended for general layout.

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Table Layout</title>
  <style>
    table, th, td {
      border: 1px solid black;
      border-collapse: collapse;
    }
    th, td {
      padding: 10px;
    }
  </style>
</head>
<body>
  <table>
    <tr>
      <th>Header 1</th>
      <th>Header 2</th>
    </tr>
    <tr>
      <td>Data 1</td>
      <td>Data 2</td>
    </tr>
  </table>
</body>
</html>

```


- Flexbox: Ideal for flexible and responsive layouts with easy alignment.

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Flexbox</title>
  <style>
    .flex-container {
      display: flex;
      justify-content: space-around;
    }
    .flex-item {
      width: 100px;
      height: 100px;
      background-color: #f0f0f0;
      margin: 10px;
    }
  </style>
</head>
<body>
  <div class="flex-container">
    <div class="flex-item">1</div>
    <div class="flex-item">2</div>
    <div class="flex-item">3</div>
  </div>
</body>
</html>

```

- Grid Layout:  Best for complex, grid-based designs requiring precise control.

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Grid Layout</title>
  <style>
    .grid-container {
      display: grid;
      grid-template-columns: 1fr 1fr 1fr;
      gap: 10px;
    }
    .grid-item {
      background-color: #f0f0f0;
      padding: 20px;
    }
  </style>
</head>
<body>
  <div class="grid-container">
    <div class="grid-item">1</div>
    <div class="grid-item">2</div>
    <div class="grid-item">3</div>
  </div>
</body>
</html>

```
