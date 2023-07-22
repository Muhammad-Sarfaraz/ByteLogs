
# HTMx
htmx is a library that allows you to access modern browser features directly from HTML, rather than using javascript.

#### htmx in a Nutshell

```javascript
<a href="/blog">Blog</a>
```

```javascript
<button hx-post="/clicked"
    hx-trigger="click"
    hx-target="#parent-div"
    hx-swap="outerHTML"
>
    Click Me!
</button>
```

#### List of request
```markdown
Attribute	Description
hx-get	Issues a GET request to the given URL
hx-post	Issues a POST request to the given URL
hx-put	Issues a PUT request to the given URL
hx-patch	Issues a PATCH request to the given URL
hx-delete	Issues a DELETE request to the given URL
```

#### Debugging
```javascript
htmx.logAll();
```
