# FB_Messenger_Watson
Combine FB Messenger bot with Watson API.

[![Node.js 4.4.5](https://img.shields.io/badge/Node.js-4.4.5-orange.svg)](https://nodejs.org/en/)
[![Platforms OS X | Windows | Linux |](https://img.shields.io/badge/Platforms-OS%20X%20%7C%20Windows%20%7C%20Linux%20-lightgray.svg)](https://nodejs.org/en/)

# What is this repository for? ###

* Quick summary: Combine FB Messenger bot with Watson API.
* Version 2.0.0

# Preparation ###

0. Read [Messengr Platform](https://developers.facebook.com/docs/messenger-platform/product-overview/setup) to know concept and flow. In this repository I demo Bot by [Botkit](https://github.com/howdyai/botkit) and [Node-RED](http://nodered.org/) separately (main funciton and reaction is in Node-RED version). You can choose one to try.

1. [Create a Facebook App](https://developers.facebook.com/quickstarts/?platform=web) and [Page](https://www.facebook.com/pages/create/) first.

2. Setup a Webhook: In the Messenger Platform tab, find the Webhooks section and click Setup Webhooks. Enter a URL for a webhook, define a `Verify Token` and select `message_deliveries`, `messages`, `messaging_optins`, and `messaging_postbacks` under Subscription Fields.

3. [Get a Page Access Token](https://developers.facebook.com/quickstarts/?platform=web): This will generate a Page Access Token with the manage_pages, pages_messaging, and pages_messaging_phone_number scopes

4. Subscribe the App to a Page in console.

# Botkit ###

* Follow by [SlackBot Repository](https://github.com/BoChengHuang/SlackBot_Watson)
* Test on local webhook url: you can use [localtunnel](https://localtunnel.github.io/www/) and [ngrok](https://ngrok.com)
* `sudo npm install` first 
* `page_token=PAGE_TOKEN verify_token=TOKEN node facebook_bot.js`
* enjoy.

# Node-RED ###

* Creat a Node-RED app on [Bluemix](https://console.ng.bluemix.net/docs/starters/Node-RED/nodered.html#nodered) first.
* Copy contents in Node-RED/FB.json
* Go to Node-RED and [import](http://developers.sensetecnic.com/article/how-to-import-a-node-red-flow/) by clipboard on menu bar.
* See a lot of nodes on flow.

1. http-in node is require for webhook validation and should send correct code and status:200 back first.
2. When msg-in http-in node will catch json data, before you handle them, you should first send status:200 back too.
3. In Detect greetings Node, I check if we need to say greetings back to users.
4. In switch node, we have 7 states.
  * State 1: get ticket template.
  * State 2: say greetings.
  * State 3 & 4: confirmation for ticket booking.
  * State 5: recognition of faces in an image by [Watson Visual Recognition api](https://www.ibm.com/watson/developercloud/doc/visual-recognition/).
  * State 6: other useless msg like watermark (prevent sending something to API).
  * State 7: send QA msg to NLP and Reasoning API and get result back.
5. Any resut shloud be encoded in json date accoding to Messenger documentation.
6. Finally send http request node to Messenger to complete the response.

Note: any API (like Watson) need API key or `usr/pwd`. If you want use NLP or Reasoning engine please contact the authur in contribution guidelines.

# How to run program ###
* Use CMD/Terminal (Botkit)
* Use web browser (Node-RED)

# Contribution guidelines ###
* [Botkit](https://github.com/howdyai/botkit)
* [fbsamples](https://github.com/fbsamples/messenger-platform-samples)
* [NLP](https://github.com/jarwow)
* [Reasoning engine](https://github.com/jimmyliao)
* Bo Cheng Huang

