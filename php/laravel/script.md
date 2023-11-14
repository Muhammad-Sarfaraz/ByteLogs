# Script

#### Store larvel exception with url and method.
```php
protected function context(): array
{
	return tap(parent::context(), function (&$context) {
	    $context = collect($context)->merge([
		'method' => request()->getMethod(),
		'url' => request()->url(),
	    ])->all();
	});
}
```

#### Json Key/Value
```php
// Set Value...
$data = ['value' => "Foo Bar"];
$jsonData = json_encode($data);
$filePath = public_path('tmp.json');
file_put_contents($filePath, $jsonData);

// Get Value...      
$jsonString = file_get_contents(public_path('tmp.json'));
$data = json_decode($jsonString);
$value = $data->value;
```


#### Get available month wise data
```php
 $monthlyCounts = JournalUser::select(
	DB::raw('MONTH(created_at) as month'),
	DB::raw('COUNT(*) as count')
	)
	->groupBy('month')
	->orderBy('month')
	->get();

$data = new Collection();

foreach ($monthlyCounts as $count) {
	$data->push([
	    'month' => Carbon::createFromDate(null, $count->month, 1)->format('F'),
	    'count' => $count->count,
	]);
}

return $result = [
	'months' => $data->pluck('month')->all(),
	'data' => $data->pluck('count')->all(),
];
```

#### Mail

- ENV
```
MAIL_MAILER=smtp
MAIL_HOST=smtp.gmail.com
MAIL_PORT=465 // For local
MAIL_USERNAME=example@gmail.com
MAIL_PASSWORD="app password" // It will be available at "https://myaccount.google.com/apppasswords?rapt=AEjHL4PHjcvdK_iZyMtNjFbNPMmnlZZo-3fpgNEY7xfTRIK9lVKLKjmXKM-PNjW6ZrFOgO3lXot_eb64lQTiglYn2umBLrhSWg", You need two-step enable first, then generate password.
MAIL_ENCRYPTION=tls
MAIL_FROM=example@gmail.com
```

#### Query of Database Example
```php
// Raw SQL
$sql = "
    SELECT COUNT(DISTINCT author_id) as count
    FROM conversations
    WHERE is_seen_by_admin IS NULL;
";

$results = DB::select($sql);
$count = $results[0]->count;

// Query Builder.
$query = DB::table('conversations')
    ->select(DB::raw('COUNT(DISTINCT author_id) as count'))
    ->whereNull('is_seen_by_admin')
    ->get();

$count = $query[0]->count;

// Eloquent
return Conversation::query()
    ->distinct('author_id')
    ->where('is_seen_by_admin', null)
    ->count();
```

#### PHP Label Go-To
```php
$counter = 1;

beginning: // Label
echo "Counter: $counter\n";
$counter++;

if ($counter <= 5) {
    goto beginning; // Jump back to the 'beginning' label
}
```

#### Get Count of Child Rows
```PHP
use Illuminate\Database\Eloquent\Builder;

$query = Album::query()->withCount(['photos','videos'])->oldest();

// Access it via.
$count = $album->photos_count;

// Closure
$album = Album::withCount([
    'photos', 
    'videos as videos_count' => function (Builder $query) {
        $query->where('status', 'published');
    }
])->get();

```

#### Show Empty Image & Make Sure Image Exist
```php
public function getPhotoAttribute($value)
{
	$defaultImage = url('/public/images/profile.webp');
	
	if (! empty($value) && Storage::exists($value)) {
	    return url('/public/storage/'.$value);
	}
	
	return $defaultImage;
}
```

#### Custom Way to Inject File in Request Instance
```php
$remoteUrl = url('/') . '/public/storage/' . $rawImage;

// Download remote file contents
$fileContents = file_get_contents($remoteUrl);

// Create a temporary file
$tmpFile = tmpfile();
fwrite($tmpFile,
    $fileContents
);

// Get file info
$tmpFileInfo = stream_get_meta_data($tmpFile);

// Create an UploadedFile instance
$uploadedFile = new UploadedFile(
    $tmpFileInfo['uri'],           // Path to the temporary file
    basename($remoteUrl),          // Original file name
    mime_content_type($tmpFileInfo['uri']), // MIME type
    filesize($tmpFileInfo['uri']), // File size
    UPLOAD_ERR_OK,                 // Error code (UPLOAD_ERR_OK indicates no error)
    true                           // Test mode (true to keep the file after the request)
);
```

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

#### If only relationship exist then fetch that row:
```php
$query = HonourBoard::query()
	->with( 'category', 'session', 'memberbody')
	->has('memberbody') // If only memberbody is exist then it will fetch that row!
	->latest();
```
