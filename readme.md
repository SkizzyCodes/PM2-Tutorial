# Pm2 Guide 2022
Pm2 is a Process Manager tool, made for Windows, Linux and Mac
## Installation
- [x] First install [nodejs v12.7 or higher (Suggested Version: 16.13)](https://github.com/Tomato6966/Debian-Cheat-Sheat-Setup/wiki/3.1-Install-nodejs-and-npm)
- [x] Then type: `npm i -g pm2`

## Starting a process
- [x] Go into the folder of the process you want to start
- [x] Type: `pm2 start index.js` (replace index.js with the file you want to start)
- [x] This also works: `pm2 start .`
- [x] `pm2 start index.js --name My_Custom_Name_Process` (replace My_Custom_Name_Process with your wished process Name, NO SPACES ALLOWED)
- [x] Option #4 is very recommended, because it gives your process a name which is shown in `pm2 list`
- [x] You can also start already stopped processes: `pm2 start ID` (replace the ID with the PROCESS Id which you get from `pm2 list`, for example: `pm2 start 1`

## View Processes
- [x] Type: `pm2 list`
- [x] This will show you all Processes, with their Name, ID and current state online/offline

Sorting them:
`pm2 list --sort name:desc` or in general `pm2 list --sort [name|id|pid|memory|cpu|status|uptime][:asc|desc]`

## Showing a specific Process
This Shows details about a specific Process
- [x] `pm2 show ID` (replace the ID with the PROCESS Id which you get from `pm2 list`, for example: `pm2 show 1`

## Stopping a Process
- [x] `pm2 stop ID` (replace the ID with the PROCESS Id which you get from `pm2 list`, for example: `pm2 stop 1`
- [x] `pm2 stop all` (this stops all processes)

You could also use the process name for this Command, but is not recommended

## Deleting a Process
- [x] `pm2 delete ID` (replace the ID with the PROCESS Id which you get from `pm2 list`, for example: `pm2 delete 1`
- [x] `pm2 delete all` (this deletes all processes)

You could also use the process name for this Command, but is not suggested

## Restarting a Process
This restarts a process, if it's already started / stopped
- [x] `pm2 restart ID` (replace the ID with the PROCESS Id which you get from `pm2 list`, for example: `pm2 restart 1`
- [x] `pm2 restart all` (this restarts all processes)

## Watching all Processes
- [x] You can either use the [Website Dashboard](https://app.pm2.io/#/register), but this only monitors / shows up to 5 processes (for free)
- [x] So use: `pm2 dash` / `pm2 monit`, there you can navigate through windows, but i would suggest you to "just" stay in the process window and use your arrow keys up and down, to show the logs of each single process

## Showing Logs
- [x] Type: `pm2 log`, this will show all pm2 logs of all processes including the process name of each process + a few older log lines
- [x] To few the logs of a specific process type:
`pm2 log ID` (replace the ID with the PROCESS Id which you get from `pm2 list`, for example: `pm2 log1`

## Restarting the System, but keeping the processes?
- [x] Very simple, before the restart type: `pm2 save`
- [x] After the restart type: `pm2 resurrect` to get the proccesses + their current states back
- [x] **ATTENTION** It is suggested to stop the processes before saving, especially if you have many, so that your vps / pc doesn't get overloaded
- [x] `pm2 stop all` --- `pm2 save` --- `pm2 resurrect`
- [x] You can type: `pm2 startup` If you don't want to use `pm2 resurrect`

## Starting Java / Python Processes
- [x] Java: `pm2 start java -- -jar JavaFile.jar`, With name: `pm2 start java --name Process_Name -- -jar JavaFile.jar`
- [x] Python: `pm2 start python` -- File.py, With name: `pm2 start python --name Process_Name -- File.py`

## Reset the ID Counters
- [x] `pm2 reset all` This resets the id, because if you deleted a process, the id don't change

## Other Useful Options
- [x] `pm2 start index.js --name Process_Name` gives the process a specific name
- [x] `pm2 start index.js --max-memory-restart 2G` change the maximum allowed memory, before the process restarts (default 100M / 1G)
- [x] `pm2 start index.js --cron-restart="0 0 * * *"` Restart the process every day at 0:0 , using [cronjob](--cron-restart="0 0 * * *")
- [x] `pm2 start index.js --watch` This auto restarts a process, on file changes
- [x] `pm2 start index.js --restart-delay=3000` Set a delay between auto restart with the Restart Delay strategy
- [x] `pm2 start index.js --no-autorestart` This is useful in case we wish to run 1-time scripts and don’t want the process manager to restart our script in case it’s completed running.
- [x] `pm2 start index.js --exp-backoff-restart-delay=100` A new restart mode has been implemented on PM2 Runtime, making your application restarts in a smarter way. Instead of restarting your application like crazy when exceptions happens (e.g. database is down), the exponential backoff restart will increase incrementaly the time between restarts, reducing the pressure on your DB or your external provider… Pretty easy to use

## Using a Configuration File
When managing multiple applications with PM2, use a JS configuration file to organize them
- [x] `pm2 init simple` This will generate a sample `ecosystem.config.js`
```javascript
module.exports = {
  apps : [{
    name   : "app1",
    script : "./app.js"
  }]
}
```
Now start the processes via: `pm2 start ecosystem.config.js` This will apply [all options](https://pm2.keymetrics.io/docs/usage/application-declaration/) inside of the file! Example completed file:
```javascript
module.exports = {
  apps : [{
    name: `Discord_Bot_Milrato_Test_Bot`, //the Namespace
    script: 'index.js', //the path where to start
    //max_restarts: 5, //to limit the maximum restarts... not suggested
    cron_restart: "0 3 * * *", //to restart at 3:00
    max_memory_restart: "1G", //restart at 1GB of Ram
    watch: true, //restart on file changes
  }]
};
```

##  Hover over the Boxes then you can copy paste it in the console, everything will be done automatically!
> *Note that if you do it without SUDO you might not have permissions to execute a specific Command*

> Make sure to be in the User: "root" by typing `su root` / `su -` / `sudo su`
