# Script

#### Get route prefix:
```
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
