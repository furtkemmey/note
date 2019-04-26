## bot name
    alert

## username
    t.me/Kemmeyalert_bot
    
## token

    881549117:AAFCnvxLfxpWyHVXWWxd780n3ZwTsQOKfTU
    
## package
    node-telegram-bot-api
    
## use
    const TelegramBot = require('node-telegram-bot-api');
    const token = '...';
    const bot = new TelegramBot(token, {polling: true});
    
## onText()
    bot.onText(/\/alert/, function (msg) {
      alert.getAlert(function(arrResult) {
        bot.sendMessage(msg.chat.id, String(arrResult));
      });
    });

## inline keyboard

    bot.onText(/\/h/, function (msg) {
      const sentMessage = 'Choose one';
      const opts = {
    		"reply_markup": {
    			"inline_keyboard": [
        			[
                      {
                        "text": "Alert"
                        ,"callback_data": "alert"            
                      }
                    ],
    			]
    		}
      }
      bot.sendMessage(msg.chat.id, sentMessage, opts); 
    });

## inline keyboard callback

    bot.on('callback_query', function(callbackData) {
      const action = callbackData.data; // This is responsible for checking the content of callback_data
      const msg = callbackData.message;
      
      switch (action) {
        case 'alert':
          alert.getAlert(function(arrResult) {
            bot.sendMessage(msg.chat.id, String(arrResult));
          });
          // bot.sendMessage(msg.chat.id, '\/alert'); 
          break;
        default:
          break;
      }
    });