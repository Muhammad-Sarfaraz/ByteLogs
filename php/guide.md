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










