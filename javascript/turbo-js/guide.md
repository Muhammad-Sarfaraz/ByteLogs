# Turbo Js Notes

##### Don't cache javascript:
```javascript
<a data-turbo="false" class="nav-link" aria-current="page" href="http://103.169.160.21/fbcci">Home</a>
```

#### Config for scroll:
```javascript
 // Turbo-js Scroll Config...
  document.addEventListener(`turbo:load`, () => {
      let initialLoading = document.getElementById("initial-loading");
      if (initialLoading) {
          initialLoading.remove();
      }
      document.documentElement.style.scrollBehavior = `smooth`

  })

  document.addEventListener(`turbo:before-visit`, () => {
      document.documentElement.style.scrollBehavior = `unset`
  })

  // Initial Loading Config...
  var isFirstLoad = true;

  if (isFirstLoad) {
      let initialLoading = document.getElementById("initial-loading");
      initialLoading.style.display = 'flex';
  }

  setTimeout(() => {
      isFirstLoad = false;
      let initialLoading = document.getElementById("initial-loading");
      if (initialLoading) {
          initialLoading.remove();
      }
  }, 1000);

  document.addEventListener('turbo:before-fetch-request', function() {
      if (isFirstLoad) {
          isFirstLoad = false;
      }

      window.scrollTo(0, 0);
      let loaderOverlay = document.getElementById('loader-overlay');
      loaderOverlay.style.display = 'flex';
  });

  document.addEventListener('turbo:render', function() {
      window.scrollTo(0, 0);
      let loaderOverlay = document.getElementById('loader-overlay');
      loaderOverlay.style.display = 'none';
  });
```
