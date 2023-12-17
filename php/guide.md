# PHP Hands On Note

#### Named Argument
```php
setcookie(
    name: 'test',
    expires: time() + 60 * 60 * 2,
);
```



#### Function default parameter value:
```php
function foo($param = 'foo')
{
    return $param;
}
$a = foo();
```

#### Grouped use statement:
```php
use Symfony\Component\HttpKernel\{
    Controller\ControllerResolverInterface,
    Exception\NotFoundHttpException,
    Event\PostResponseEvent,
};
```

#### Union type:
```php
function myFunction(string|int|array $param): string|int|array
{
    return $param;
}
```

#### Nullable type:
```php
function foo($param)
{
    return $param;
}
$a = foo(null);
```



#### Elvis operator
```php
$a = null;
$b = $a ?: 'fallback';
```


#### Short colusure:
```php
fn foo($bar) => $bar + 1;
```



#### Nullsafe operator:
```php
$a = null;
$b = $a?->foo;
// $b = null
$c = $a?->foo();
// $c = null
```


#### Everyday Use Case:

###### IF/ELSE

```php
 $content = $response instanceof BinaryFileResponse
            ? $response->getFile()->getContent()
            : $response->getContent();
```

###### Pipeline
```php
 return (new Pipeline)->send($request)
    ->through([
        new EnsureOnNakedDomain,
        new RedirectStaticAssets,
        new EnsureVanityUrlIsNotIndexed,
        new EnsureBinaryEncoding(),
    ])->then(function ($request) use ($context) {
        static::$worker->handle($request, $context);
        return static::$response->response;
    });
```

###### Tap

```php
return tap(new Response(
    $content,
    $response->headers->all(),
    $response->getStatusCode()
), static function () {
    static::$response = null;
});
```

###### Use Pointer

```php
if (empty($segment = substr($segment, 0, -1))) {
    $pointer = &$pointer[];
}
```  


###### Mono Static
```php
static::$logger = new MonologLogger('vapor', [
    (new StreamHandler('php://stderr'))->setFormatter(new JsonFormatter),
]);
```

###### Tap and static

```php
return tap(static::all($path, (array) $parameters), function ($variables) {
    foreach ($variables as $key => $value) {
        echo "Injecting secret [{$key}] into runtime.".PHP_EOL;

        $_ENV[$key] = $value;
        $_SERVER[$key] = $value;
    }
});
```

#### Brief About Json In PHP

* JsonSerializable
```php
<?php
class User implements JsonSerializable {
    private $username;
    private $email;

    public function __construct($username, $email) {
        $this->username = $username;
        $this->email = $email;
    }

    public function jsonSerialize() {
        return ['username' => $this->username];
    } 
}

$user = new User('john_doe', 'john@example.com');
echo json_encode($user);  // Output: {"username":"john_doe"}

```

* json_encode()
```php
$obj = new stdClass();
$obj->id = 1;
$obj->age = 30;
$obj->city = 'New York';

$jsonString = json_encode($obj);

echo $jsonString;

// PHP Array
$personArray = array(
    'name' => 'John',
    'age' => 30,
    'city' => 'New York'
);

// Encode PHP array into a JSON string
$jsonString = json_encode($personArray);

// Output JSON string
echo $jsonString;
```

* json_decode()
```php
<?php
// JSON string
$jsonString = '{"id":1,"country_id":30,"city":"New York"}';

// Decode JSON string into a PHP object
$data = json_decode($jsonString);

// Accessing properties
echo "Id: " . $data->id . "<br>";
echo "Country Id: " . $data->country_id . "<br>";
echo "City: " . $data->city . "<br>";

$data = json_decode($jsonString,true); // Associative array
echo "<br>"."City: " . $data['city'] . "<br>";
```

#### Working with json:
```
// Load the contents of the JSON files
    $districtOldData = json_decode(File::get(database_path('districtOld.json')), true,512, JSON_UNESCAPED_UNICODE);
    $districtNewData = json_decode(File::get(database_path('districtNew.json')), true, 512, JSON_UNESCAPED_UNICODE);
    $thanasData = json_decode(File::get(database_path('thanas.json')), true, 512, JSON_UNESCAPED_UNICODE);

    $thanas = [];

    // Process each district from districtOld.json
    foreach ($districtOldData as $oldDistrict) {
        $oldDistrictName = $oldDistrict['name'];

        // Search for the district with the same name in districtNew.json and retrieve its ID
        $matchingDistrictNew = collect($districtNewData)->firstWhere('name', $oldDistrictName);

        $districtNewId = $matchingDistrictNew ? $matchingDistrictNew['id'] : null;

        $districtbanglaName = $matchingDistrictNew ? $matchingDistrictNew['bn_name'] : null;

        $data = [];
        // Replace the corresponding district ID in thanas.json
        foreach ($thanasData as &$thana) {

            if ($thana['district_id'] == $oldDistrict['id']) {


                //dd([$oldDistrictName, $districtbanglaName], $thana['district_id'] == $oldDistrict['id'], $thana['district_id'] , $districtNewId);
                $thana['district_id'] = $districtNewId;
                 $data['newId'] = $districtNewId;
                $thanas[] = $thana;
            }else{
                //dd($thana['district_id'] , $oldDistrict['id'],$thana, $oldDistrict, $districtbanglaName, $districtNewId);
            }
        }
    }
    // Save the modified thanas.json file
    File::put(database_path('thanas-update.json'), json_encode($thanas, JSON_UNESCAPED_UNICODE | JSON_PRETTY_PRINT));

    return "District ID replacement for all districts completed successfully.";
```





