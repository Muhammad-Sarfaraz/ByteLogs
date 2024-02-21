# Typescript

#### Installation:
Globally install the typescript:

```  npm i -g typescript ```

Ts-Node:

``` npm install -g ts-node typescript '@types/node' ```

Run Typescript:

``` ts-node typescript.ts ```

Watch Mode:

``` tsc typescript.ts --watch ```

What if you have more than 1 file:
```
tsc --init
tsc -w
```


#### Types



#### Disbale type checking
Setting any to the special type any disables type checking:

```typescript 
let v: any = true;
```
