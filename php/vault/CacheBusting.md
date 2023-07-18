# Cache Busting

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
