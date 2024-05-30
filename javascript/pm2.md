# PM2

PM2 is a daemon process manager that will help you manage and keep your application online.

#### Start an app
```bash
pm2 start app.js
```

#### Display Logs

Display logs
To display logs in realtime:

```sh
$ pm2 logs
```

To dig in older logs:

```sh
$ pm2 logs --lines 200
```


#### Terminal Based Dashboard
Here is a realtime dashboard that fits directly into your terminal:

```sh
$ pm2 monit
```

#### Cluster mode
For Node.js applications, PM2 includes an automatic load balancer that will share all HTTP[s]/Websocket/TCP/UDP connections between each spawned processes.

To start an application in Cluster mode:

```sh
$ pm2 start app.js -i max
```

#### Run in Seperate Port
```sh
PORT=5000 pm2 start dist/main.js -f
```

#### Set a name project
```
--name <app_name>
```

#### Managing processes
Managing application state is simple here are the commands:

```
$ pm2 restart app_name
$ pm2 reload app_name
$ pm2 stop app_name
$ pm2 delete app_name
```

#### Cheatsheet
CheatSheet
Here are some commands that are worth knowing. Just try them with a sample application or with your current web application on your development machine:

# Fork mode
```
pm2 start app.js --name my-api # Name process
```

# Cluster mode
```
pm2 start app.js -i 0        # Will start maximum processes with LB depending on available CPUs
pm2 start app.js -i max      # Same as above, but deprecated.
pm2 scale app +3             # Scales `app` up by 3 workers
pm2 scale app 2              # Scales `app` up or down to 2 workers total
```

# Listing

```
pm2 list               # Display all processes status
pm2 jlist              # Print process list in raw JSON
pm2 prettylist         # Print process list in beautified JSON

pm2 describe 0         # Display all information about a specific process

pm2 monit              # Monitor all processes
```

# Logs

```
pm2 logs [--raw]       # Display all processes logs in streaming
pm2 flush              # Empty all log files
pm2 reloadLogs         # Reload all logs
```

# Actions

```
pm2 stop all           # Stop all processes
pm2 restart all        # Restart all processes

pm2 reload all         # Will 0s downtime reload (for NETWORKED apps)

pm2 stop 0             # Stop specific process id
pm2 restart 0          # Restart specific process id

pm2 delete 0           # Will remove process from pm2 list
pm2 delete all         # Will remove all processes from pm2 list
```

# Misc

```
pm2 reset <process>    # Reset meta data (restarted time...)
pm2 updatePM2          # Update in memory pm2
pm2 ping               # Ensure pm2 daemon has been launched
pm2 sendSignal SIGUSR2 my-app # Send system signal to script
pm2 start app.js --no-daemon
pm2 start app.js --no-vizion
pm2 start app.js --no-autorestart
```
