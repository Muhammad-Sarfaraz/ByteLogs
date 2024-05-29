# PM2

PM2 is a daemon process manager that will help you manage and keep your application online.

#### Start an app
```
pm2 start app.js
```

#### Display Logs

Display logs
To display logs in realtime:

```
$ pm2 logs
```

To dig in older logs:

```
$ pm2 logs --lines 200
```


#### Terminal Based Dashboard
Here is a realtime dashboard that fits directly into your terminal:

```
$ pm2 monit
```