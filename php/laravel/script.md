# Script

#### Multiple unique input validation:
```php

// AppServiceProvider.php
use Illuminate\Support\Facades\Validator;

Validator::extend('unique_combination', function ($attribute, $value, $parameters, $validator) {
	$twoValue = $validator->getData()[$parameters[0]];
	$threeValue = $validator->getData()[$parameters[1]];
	return ($value != $twoValue || $value != $threeValue) && ($twoValue != $threeValue);
});

// In your controller
request()->validate([
    'first_choice' => 'required|unique_combination:second_choice,third_choice',
    'second_choice' => 'nullable',
    'third_choice' => 'nullable',
],[
    'unique_combination' =>
    'Please select unique committees. Multiple same committees are prohibited.',
]);

```

#### Check query time:
```
$start = microtime(true);
$data['members'] = $member->paginate(intval(config('app.PAGINATE_LIMIT')))
    ->appends(request()->query());
$data['queryTime'] = number_format((microtime(true) - $start), 4);
```

#### If only relationship date exist them fetch that row:
```php
$query = HonourBoard::query()
	->with( 'category', 'session', 'memberbody')
	->has('memberbody') // If only memberbody is exist then it will fetch that row!
	->latest();
```
