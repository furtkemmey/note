# PM2

## install
    npm i pm2 -g

## start
    pm2 start -i max --name alert app.js
    // -i number of process or max
    
## list
    pm2 list
    
## stop
    pm2 stop [name] or [id]
    pm2 stop all
    
## delete
    pm2 delete [name] or [id]
    pm2 delete all
    
## reload
    pm2 reload [name] or [id] or all
## restart
    pm2 restart
    pm2 restart all
    
##  monit
    pm2 monit

## config.json
    pm2 start config.json
    
    {
      "apps" : [
        {
          "name"        : "telegramBot",  
          "script"      : "./app.js",
          "watch": false,
          "ignore_watch" : [ 
            "node_modules", 
            "logs",
            "public"
          ],
          "watch_options": {
            "followSymlinks": false
          },
          "error_file" : "./logs/app-err.log",  
          "out_file"   : "./logs/app-out.log",  
          "env": {
              "NODE_ENV": "development"
          }
        }
      ]
    }

#loadtest

## install
    npm i -g loadtest

## run test
    loadtest -n 1000 -c 100 http://192.168.192.112:8081/
    // -n 發射總數
    // -c 發射級數
    loadtest -c 100 --rps 200 http://192.168.192.112:8081/