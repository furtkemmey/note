# forever

## install
    npm i -g forever
    
## start
    forever start  app.js
    forever --uid "app1" start app.js

## list
    forever list

## restart
    forever restart app.js
            restartall

##  stop 
    forever stop [forever pid]
    forever stopall
    
## web gui
    git clone https://github.com/FGRibreau/forever-webui.git
    cd forever-webui/
    npm install
    node add_user.js
    node app.js
    http://192.168.192.112:8085/