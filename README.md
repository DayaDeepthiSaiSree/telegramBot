# telegramBot
const request = require('request');




const TelegramBot = require('node-telegram-bot-api');

const token = '5504809322:AAFSy7v7ouKTcgjy8m3CaVOhUbzeqyBajUU';
const bot = new TelegramBot(token ,{polling:true});
        bot.on('message', function(mg){
          request('http://www.omdbapi.com/?t='+mg.text+'&apikey=c6c1d823', function (error, response, body) {
              console.log(mg);
              console.log(body);
              if(mg.text == '/start'){
                  bot.sendMessage(mg.chat.id,"WELCOME, enter a movie name to it's details.");
              }
              else if(JSON.parse(body).Response=="True"){
              
              bot.sendMessage(mg.chat.id, "Title : "+JSON.parse(body).Title);
              bot.sendMessage(mg.chat.id, "Year : "+JSON.parse(body).Year);
              bot.sendMessage(mg.chat.id, "Director : "+JSON.parse(body).Director);
              bot.sendMessage(mg.chat.id, "Actor : "+JSON.parse(body).Actors);
              bot.sendMessage(mg.chat.id, "Writer : "+JSON.parse(body).Writer);
              bot.sendMessage(mg.chat.id, "Plot : "+JSON.parse(body).Plot);
              bot.sendMessage(mg.chat.id, "Runtime : "+JSON.parse(body).Runtime);
              
          }
          else{
              bot.sendMessage(mg.chat.id, "Movie not found :(");
          }
      
      })
      });
