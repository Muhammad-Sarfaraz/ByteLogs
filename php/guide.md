# PHP Hands On Note

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
```
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





