Heimdall
=========
Heimdall is a bot which bridges a chat in [Telegram](https://telegram.org) with a channel in [Discord](https://discordapp.com/).

There is no public Heimdall bot. You need to host it yourself. To host a bot, you need [nodejs](https://nodejs.org). The bot requires NodeJS 8 or higher


Step by step installation:
--------------------------

 1. Install latest Nodejs and NPM.
    `sudo apt-get update`
    `apt-get install build-essential libssl-dev`
    `curl https://raw.githubusercontent.com/creationix/nvm/v0.33.11/install.sh | bash`
    `source ~/.profile`
    `nvm install 10`
    `npm install -g npm`

 2. Clone this repo.
    `git clone https://github.com/HodlerCompany/Heimdall`

 3. Open a terminal and enter the repo with the [`cd`](https://en.wikipedia.org/wiki/Cd_(command)) command. Something like `cd Downloads/Heimdall`. Your exact command may differ.

 4. Run the command `npm install`

 5. Make a copy of the file `example.settings.yaml` and name it `settings.yaml`

 6. Aquire a bot token for Telegram ([How to create a Telegram bot](https://core.telegram.org/bots#3-how-do-i-create-a-bot)) and put it in the settings file
   - The Telegram bot must be able to access all messages. Talk to [@BotFather](https://t.me/BotFather) to disable privacy mode for the bot
   - Do NOT use another bot you already have running. That will cause all sorts of weird problems. Make a new one

 7. Aquire a bot token for Discord ([How to create a Discord bot](https://github.com/reactiflux/discord-irc/wiki/Creating-a-discord-bot-&-getting-a-token)) and put it in the settings file under `discord.token`. **NOTE** that the token is NOT the "Client Secret". The token is under the section "App bot user" further down the page
   - Do NOT use another bot you already have running. That will cause all sorts of weird problems. Make a new one.

 8. Add the Telegram bot to the Telegram chat
   - If the Telegram chat is a supergroup, the bot also needs to be admin of the group, or it won't get the messages. The creator of the supergroup is able to give it admin rights.

 9. Add the Discord bot to the Discord server (https://discordapp.com/oauth2/authorize?client_id=YOUR_CLIENT_ID_HERE&scope=bot&permissions=248832). This requires that you have admin rights on the server.

 10. Start Heimdall: `npm start`

 11. Ask the bots for the remaining details. In the Telegram chat and the Discord channel, write `/chatinfo`. Put the info you get in the settings file.
   - If you want to bridge a Telegram group or channel, remember that the ID is negative. Include the `-` when entering it into the settings file
   - It is important that the Discord IDs are wrapped with single quotes when entered into the settings file. `'244791815503347712'`, not `244791815503347712`

 12. Restart Heimdall. You stop it by pressing CTRL + C in the terminal it is running in

Done! You now have a nice bridge between a Telegram chat and a Discord channel

*********************************************************

FAQ
---

### What kind of machine do I need to run this?

Anything capable of running [NodeJS](https://nodejs.org) should be able to run TediCross. People have had success running it on ordinary laptops, raspberry pis, Amazon Web Services, Google Cloud Platform, and other machines. It runs on both Linux and Windows, and probably also macOS. It does NOT, however, run on [Heroku](https://heroku.com)

The machine must be on for Heimdall to work


### When running `npm install`, it complains about missing dependencies?

The [Discord library](https://discord.js.org/#/) Heimdall is using has support for audio channels and voice chat. For this, it needs some additional libraries, like [node-opus](https://www.npmjs.com/package/node-opus), [libsodium](https://www.npmjs.com/package/libsodium) and others. Heimdall does not do audio, so these warnings can safely be ignored

### How do I create more bridges?

Heimdall supports a theoretically infinite number of bridges, limited only by your hardware. Even a simple Raspberry Pi is powerful enough to run multiple bridges, so don't worry about making more

To make more bridges, just copy the one you have, paste it right below and make necessary changes:

```
...
bridges:
  - name: Default bridge
    direction: both
    telegram:
      ...
    discord:
      ...
  - name: Another bridge
    direction: both
    telegram:
      ...
    discord:
      ...
...
```

The names of the bridges are practically only log identifiers. They can be whatever string you want them to be. Note, however, that the setting `discord.skipOldMessages` uses the names to know which messages was last sent from which channel, so they should be unique.

Note that the settings file is indentation sensitive. If you do for example
```
  - name: Bridge 1
      direction: both
```
it won't work. The "d" in "direction" must be directly below the "n" in "name". See `example.settings.yaml` for proper indentation

### How do I make the bot run automatically when my computer/server starts?

Take a look in [guides/autostart/](guides/autostart/) of this repo


### How do I update Heimdall?

If you cloned the git repo, just do a `git pull`. Running `npm install` may or may not be necessary. It doesn't hurt to run it anyway



----------------

This repo has been forked from TediCross. 

https://github.com/TediCross/TediCross

Cryptocoins of the following types are accepted for donation:

* BTC: 1Gzr9ZyvTiFCPKfy2BshuZgUeFLebAfbFU
* ETH: 0x9449D54C85C8FdB079e74379d93A9C9fe611981A
