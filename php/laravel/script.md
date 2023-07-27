# Script

#### Filters [Search with thousand Parameter]:
```app/Filters/Employee/EmployeeSearchFilter.php```
```php

<?php

namespace App\Filters\Employee;
use Closure;

class EmployeeSearchFilter
{
    public function handle($query, Closure $next )
    {
        if (!empty(request('name'))) {
            $query->whereLike('name', request('name'));
        }
        return $next($query);
    }
}
```
```In model```
```php
public function scopeFilter($query, EmployeeSearchFilter $filters)
{
	return $filters->handle($query, function ($query) {
	    return $query;
	});
}
```
``` In controller ```
```php
$query = Employee::query()
    ->with(['rank', 'organization', 'employeeType'])
    ->filter(new EmployeeSearchFilter())
    ->get();
```

#### Multiple unique input validation:
``` AppServiceProvider.php ```
```php
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

#### Invoable class:

``` Example-01 ```
```php
$path = (new HospitalAction)($path);


class HospitalAction{

 public function __invoke($path)
 {
   return $path;
 }
}
```

``` Example-02 ```
```
Route::get('hospital',HospitalController::class)->name('hospital.path');

class HospitalController{

 public function __invoke($path)
 {
   return $path;
 }
}
```

#### Laravel cache:
```php
$versions = Cache::remember('laravel-versions', 3600, function () {
    return Hospital::orderBy('major', 'desc')->orderBy('minor', 'desc')->get();
});
```

#### Get route prefix:
```php
return request()->route()->getPrefix();
```

#### Remove global scopes from model:
```php
User::withoutGlobalScope(AgeScope::class)->get();

return Hospital::withoutGlobalScope('first')->where([
    'emergency' => $semver->major,
    'icu' => $semver->minor,
    'general' => $semver->patch,
])->firstOrFail();
```

#### Check query time:
```php
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
