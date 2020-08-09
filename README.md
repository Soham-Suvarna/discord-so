# discord-so
A powerful module with so many features like memes, automemes, chatbot & more. The original package made by Snowflake was removed, so I added it again.

[![NPM](https://nodei.co/npm/discord-so.png)](https://nodei.co/npm/discord-so/)

# Features
- Posting memes to discord directly
- Fetching random memes from reddit
- Cat, Dog, Bird images
- Emojify endpoint for discord
- Cowsay
- Roast, jokes, eightball, discord welcome messages
- Easy to use
- Lightweight

# Functions
- meme
- postAutoMemes
- enableMemeEvent
- cat
- bird
- dog
- fortune
- emojify
- chat
- cowsay
- roast
- discordWelcomeMessages
- eightball
- shuffle
- joke
 
# Docs
## Installing
```
npm i --save discord-so
```

## Getting Started
```js
const { DSO } = require("discord-so");
const dso = new DSO();
```

## Fetching Random Memes
```js
const { DSO } = require("discord-so");
const dso = new DSO();
dso.enableMemeEvent(7000, ["me_irl", "Dankmemes", "funny"]); /* 7000 => interval | ["me_irl", "Dankmemes", "funny"] => Redditors || Enables MEME_GET event */

dso.on("MEME_GET", (meme) => {
  if (meme.nsfw || meme.isVideo) return;
  console.log(meme.imageURL);
});
```

## Discord.js Random Memes Post
```js
const { Client, MessageEmbed } = require("discord.js");
const client = new Client();

const { DSO } = require("discord-so");
const dso = new DSO();
dso.enableMemeEvent(7000, ["me_irl", "Dankmemes", "funny"]); /* 7000 => interval | ["me_irl", "Dankmemes", "funny"] => Redditors || Enables MEME_GET event */


dso.on("MEME_GET", (meme) => {
  if (meme.nsfw || meme.isVideo) return;
  const embed = new MessageEmbed()
  .setImage(meme.imageURL)
  .setTitle("New Meme")

  client.channels.get("channel_id").send(embed);
});

client.login("Token Goes Here");
```

## Meme Autopost Function
```js
const { Client } = require("discord.js");
const client = new Client();
const { DSO } = require("discord-so");
const dso = new DSO();

client.on("ready", () => {
    console.log("ready!");
    let memechannel = client.channels.get("meme_channel_id");
    dso.PostAutoMemes(memechannel, 7000, ["PewdiepieSubmissions", "Dankmemes", "me_irl"], { includeNSFW: false }); // posts random memes to a channel in every 7 seconds
});

client.login("Token Goes Here");
```
## Example
```js
const { Client } = require("discord.js");
const client = new Client();
const { DSO } = require("discord-so");
const dso = new DSO();
const fact = DSO.randomFact
const quotes = DSO.quote

client.on("ready", () => {
    console.log("ready!");
    let memechannel = client.channels.get("meme_channel_id");
    dso.PostAutoMemes(memechannel, 7000, ["PewdiepieSubmissions", "Dankmemes", "me_irl"], { includeNSFW: false });
});

client.on("message", (message) => {
    if (!message.guild || message.author.bot) return;
    const prefix = "!";
    if (!message.content.startsWith(prefix)) return;
    let args = message.content.slice(prefix.length).trim().split(" ");
    let command = args.shift().toLowerCase();
    
    if (command === "ping") {
        return message.channel.send("pong");
    } else if (command === "emojify") {
        let msg = dso.emojify(args.join(" "));
        return message.channel.send(msg);
    } else if (command === "meme") {
        dso.meme(message.channel, ["me_irl", "Dankmemes"], { readyMade: true });
    } else if (command === "fact") {
        return message.channel.send(fact)
    } else if (command === "quote") {
        return message.channel.send(quotes)
    } 
});

client.login("Token Goes Here");
```