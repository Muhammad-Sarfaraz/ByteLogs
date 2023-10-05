# Validating the HTML Form

#### Using Parsley
```url
https://github.com/guillaumepotier/Parsley.js
```

#### Boilerplate
```html

<script src="https://code.jquery.com/jquery-3.7.1.js"
integrity="sha256-eKhayi8LEQwp4NKxN+CfCh+3qOVUtJn3QNZ0TciWLP4=" crossorigin="anonymous"></script>
<script src="parsley.min.js"></script>

<form id="demo-form" data-parsley-validate="" method="post" action="/">
  <label for="fullname">Full Name * :</label>
  <input type="text" class="form-control" name="fullname" required="">
  <label for="email">Email * :</label>
  <input type="email" class="form-control" name="email" data-parsley-trigger="change" required="">
  <input type="submit" class="btn btn-default" value="validate">
</form>

<script type="text/javascript">
$(function () {
  $('#demo-form').parsley().on('field:validated', function() {
    var ok = $('.parsley-error').length === 0;
    $('.bs-callout-info').toggleClass('hidden', !ok);
    $('.bs-callout-warning').toggleClass('hidden', ok);
  })
  .on('form:submit', function() {
    return true; // True -> It will trigger post request.
  });
});
</script>
```

#### Built in Method
- Required: data-parsley-required
- Email: data-parsley-type="email"
- Number: data-parsley-type="number"
- Integer: data-parsley-type="integer"
- Digit: data-parsley-type="digits"
- Url: data-parsley-type="url"
- Max Length: data-parsley-maxlength="10"
- Length: data-parsley-length="[6, 10]", minlength="6" maxlength="10"
- Range: data-parsley-range="[6, 10]"
- Equalto: data-parsley-equalto="#anotherfield"

#### Custom Field
```html
<input type="text" data-parsley-multiple-of="3" />

<script>
window.Parsley
.addValidator('multipleOf', {
  requirementType: 'integer',
  validateNumber: function(value, requirement) {
    return 0 === value % requirement;
  },
  messages: {
    en: 'This value should be a multiple of %s',
    fr: 'Cette valeur doit être un multiple de %s'
  }
});
</script>

```

#### Custom Error on Field
```html
data-parsley-error-message="my message"
```

#### Event
```js
$('#some-input').parsley().on('field:success', function() {
  // In here, `this` is the parlsey instance of #some-input
});
```
