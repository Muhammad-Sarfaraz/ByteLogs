# Caching
 The process of temporarily storing frequently accessed data to enhance performance and reduce the need for repetitive data retrieval.

 ***Code Example:***
 ```php
Copy code
// Function to get data from cache or original source
function getData() {
    $cacheFile = 'cache.txt';

    // Check if data is cached
    if (file_exists($cacheFile) && (time() - filemtime($cacheFile) < 3600)) {
        // Retrieve data from cache
        return file_get_contents($cacheFile);
    } else {
        // Retrieve data from original source
        $data = 'Data from original source';

        // Save data to cache file
        file_put_contents($cacheFile, $data);

        return $data;
    }
}

// Usage
$result = getData();
echo $result;
```
