# Hands on Note on REGEX:

#### Vscode:

```
Ex: "40"
Search : "district_id"\s*=>\s*"(\d+)"
Replace With: "district_id" => $1
Output: 40
```

#### Short Smaller Character
```
"^[a-z0-9_\-]+$"
```

###### Replace the line:
```
Ex:"id" => 1,
^\s*"id"\s*=>\s*\d+.*$
Output: you define
```

#### Only Allow [abcdf]
```
^[abcdf]+$
```
