---
description: Connect your own chatbots to Tiledesk
---

# Hello World tutorial for external chatbots integration

Tiledesk is designed to allow external chatbots to easy communicate with your Agents or End users. Once a chatbot receive an authenticationn token from Tilesk he can easily call many APIs to modify the state of a Request \(the support conversation\) changing Departments, inviting Agents, sending scheduled messages, use the chatbot microlanguage to simplify interaction with buttons, images, messages' timing etc.

This tutorial will show you how to create a very basic chatbot integration, allowing you to reply to specific messages sent by the End user.

## Signup a user on Tiledesk

To use Tiledesk APIs or integrate your own chatbots is mandatory to signup a new user on our beta environment. It's available on the following link [https://support-pre.tiledesk.com/dashboard](https://support-pre.tiledesk.com/dashboard)

**The previous APIs end-point will change as soon as the beta version will be released as Tiledesk v2. This tutorial will be updated accordingly.**

![](../../.gitbook/assets/image%20%2832%29.png)

After signup please follow the proposed wizard to create your first Tiledesk project.

![](../../.gitbook/assets/image%20%288%29.png)

We can jump the next step, relative to the widget installation. We will use the widget later.

Now you will jump in the project home.

To integrate an external bot, we'll need a web endpoint where all the chatbot's requests will be forwarded. We'll use the well-known Repl.it service to fast create our own web endpoint.

Go on [the repl.it](https://repl.it/~) and press "+ new repl" button. Then select NodeJS as the programming environment and choose a unique name of you repl propject. in this case _tiledeskbot_, that obviously you can't use before it was already taken for this tutorial :\)

![](../../.gitbook/assets/image%20%2829%29.png)

Now push on the **examples** link in the generated code. A popup like the following will open. Choose the  "Server \(Express\)" option.

![](../../.gitbook/assets/image%20%2825%29.png)

Your source code will change, like the following:

![](../../.gitbook/assets/image%20%2849%29.png)

We'll use **NodeJS** and Express framework for this example, due to their semplicity, low cost hosting and low learning curve. But keep in mind that the concepts in this tutorial can be easily applied to every web framework of your choice.

As soon as the _repl_ project is ready you will see something like this:

![](../../.gitbook/assets/image%20%2857%29.png)

Now we can add a new HTTP method POST to our web application, lets call this /bot, so the code will look like this:

 

![](../../.gitbook/assets/image%20%2842%29.png)

We can reach this url using the full address \(with HTTP POST method\):

[https://tiledeskbot.andreasponziell.repl.co/bot](https://tiledeskbot.andreasponziell.repl.co/bot)

We call the previuos url **external bot address service**. We'll use this later.

Now open the **Settings** menù on the left panel of our Tiledesk project, selecting the **Bots** option

![](../../.gitbook/assets/image%20%2823%29.png)

Press the ADD BOT button, to create your own external bot.

We must chose a name for our bot, set the "External" checkbox, and finally placing in the Url field the **external bot address service** from repl:

![](../../.gitbook/assets/image%20%2811%29.png)

Click the CREATE BOT button.

![](../../.gitbook/assets/image%20%2850%29.png)

Tolobot is now available in our summary list.

![](../../.gitbook/assets/image%20%2844%29.png)

It's time to write some code to make our bot service functional.

Go back to the repl project. In the index.js file modify the **/bot** service, copying and pasting the following code:

```text
const express = require('express');
const bodyParser = require('body-parser');
const request = require('request');

const app = express();
app.use(bodyParser.json());

app.get('/', (req, res) => {
  res.send('Hello Express app!')
});

app.post('/bot', (req, res) => {
  let body = req.body;
  let token = body.token;
  let enduser_text = body.payload.text;
  let tiledesk_request = body.payload.request;
  let project_id = body.payload.id_project;
  let request_id = tiledesk_request.request_id
  let bot_name = tiledesk_request.department.bot.name;
  
  // immediatly reply to TILEDESK
  res.status(200).send({"success":true});

  const endpoint =
    "https://tiledesk-server-pre.herokuapp.com";
    
  // Reply service is asynchronous.
  // Once you get the request token you can write to this
  // conversation as many times as you want
  let msg = {
    "text": "Hello from chatbot!",
    "type": "text",
    "senderFullname": bot_name // or whatever you want
  }
  
  request({
    url: `${endpoint}/${project_id}/requests/${request_id}/messages`,
    headers: {
      'Content-Type' : 'application/json',
      'Authorization': 'JWT '+token
    },
    json: msg,
    method: 'POST'
    },
    function(err, res, resbody) {
      console.log("Message sent.")
    }
  );
  
})

app.listen(3000, () => {
  console.log('server started');
});
```

The APIs endpoint in the code:

```text
https://tiledesk-server-pre.herokuapp.com
```

Is temporary and will change as soon as **Tiledesk v2** will be released. This tutorial will be updated accordingly.

You can find the full code of thihs tutorial on the repl linked here [https://repl.it/@andreasponziell/tiledeskbot](https://repl.it/@andreasponziell/tiledeskbot) 

Now that our code is ok, we should configure a routing rule to make this chatbot available to our users. Select the **Routing** option and configure the corresponding rules as follows, activating the Bot, selecting Tolobot and marking the **Bot only** option for this routing, so **Tolobot will be the only available Agent**.

![](../../.gitbook/assets/image%20%2836%29.png)

To test our chhatbot go to the **Requests** menù and press the green "Simulate visitor" button as shown in the following figure.

![](../../.gitbook/assets/image%20%2841%29.png)

A new browser Tab will open with the widget working as if it is already installed on your website.

 

![](../../.gitbook/assets/image%20%2854%29.png)

Push the **New conversation** button. A new conversation will open on the default routing. A hidden message is sent to your bot, if activated \(as in our example\). Your bot will reply with the message you previously configured in the code:

![](../../.gitbook/assets/image%20%286%29.png)

In the next tutorial you will learn how to interact with the Request directly from your chatbot code, asking the end user for his fullname and email before continuing the conversation.
