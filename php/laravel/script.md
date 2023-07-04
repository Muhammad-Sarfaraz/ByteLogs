# Script

#### If only relationship date exist them fetch that row:
```
	$query = HonourBoard::query()
        ->with( 'category', 'session', 'memberbody')
        ->has('memberbody') // If only memberbody is exist then it will fetch that row!
  ->latest();
```
