# PHP Hands On Note

#### Design Pattern:
###### Service Pattern:

#### Function default parameter value:
```
function foo($param = 'foo')
{
    return $param;
}
$a = foo();
```

#### Grouped use statement:
```
use Symfony\Component\HttpKernel\{
    Controller\ControllerResolverInterface,
    Exception\NotFoundHttpException,
    Event\PostResponseEvent,
};
```

#### Union type:
```
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
```
$a = null;
$b = $a ?: 'fallback';
```


#### Short colusure:
```
fn foo($bar) => $bar + 1;
```



#### Nullsafe operator:
```
$a = null;
$b = $a?->foo;
// $b = null
$c = $a?->foo();
// $c = null
```


#### Everyday:

###### IF/ELSE

```
 $content = $response instanceof BinaryFileResponse
            ? $response->getFile()->getContent()
            : $response->getContent();
```

###### Pipeline
```
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

```
return tap(new Response(
            $content,
            $response->headers->all(),
            $response->getStatusCode()
        ), static function () {
            static::$response = null;
        });
```

###### Use Pointer

```
if (empty($segment = substr($segment, 0, -1))) {
    $pointer = &$pointer[];
}
```  


###### Mono Static
```
static::$logger = new MonologLogger('vapor', [
    (new StreamHandler('php://stderr'))->setFormatter(new JsonFormatter),
]);
```

###### Tap and static

```
return tap(static::all($path, (array) $parameters), function ($variables) {
    foreach ($variables as $key => $value) {
        echo "Injecting secret [{$key}] into runtime.".PHP_EOL;

        $_ENV[$key] = $value;
        $_SERVER[$key] = $value;
    }
});
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





