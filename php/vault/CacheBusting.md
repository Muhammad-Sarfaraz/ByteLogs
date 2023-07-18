# Cache Busting

Cache busting is a technique used to force the browser to fetch the latest version of a file by appending a unique parameter to its URL. Here's a single-line example of cache busting:

html
Copy code

```php

$file = "js/script.js" // asset('js/script.js');

function cache_busting($file)
{
    if( file_exists(public_path($file)) ){
        $timestamp = filemtime(public_path($file));
        $version = "?version=" . md5($timestamp);

        return ($version);
    }

    $alternative = "?version=" . md5(time());
    return $alternative;
}
```
