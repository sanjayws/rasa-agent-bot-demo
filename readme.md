
# Chatwoot Agent Bot Demo using Botpress

This is a sample implementation of agent bot capabilities in chatwoot using [rasa](https://botpress.com/) . Botpress is an Open Source is a machine learning framework to automate text assistants.

You can refer the [botpress documentation](https://botpress.com/docs) to get it up and running in your machine. 

This implementation isn't a recommended set up for production, but just to illustrate the capabilities of the platform. Please build on top of this ideas discussed to have in running in production.

## Install Botpress (for dev environment only). 

```
#download latest botpress
mkdir botpress
wget https://s3.amazonaws.com/botpress-binaries/botpress-v12_26_7-linux-x64.zip
unzip botpress-v12_26_7-linux-x64.zip
./bp --serve
```

##  Get your chatwoot up and create an agent bot

go to your chatwoot directory and ensure your local server is running.  Start a rails console in your directory.

```
bundle exec rails c
```

Inside the rails console, type the following commands to create an agent bot and get its access token. Save the retrieved token as you would need it in further step.

```
bot = AgentBot.create!(name: "Botpress Bot", outgoing_url: "http://localhost:8000")
bot.access_token.token
```

Connect Agent Bot to your inbox by running the following command

```
AgentBotInbox.create!(inbox: Inbox.first, agent_bot: bot)
```

## Clone this repo into your machine and run the rasa router script. 

clone repo using the following command. 

```
git clone git@github.com:chatwoot/rasa-agent-bot-demo.git
```

open up the `rasa-router/index.php` file in your editor and change the follow values with appropriate ones. 

```
$rasa_url = 'http://localhost:5005';
$chatwoot_url = 'http://localhost:3000';
$chatwoot_bot_token = '<your agent bot token>';
```

run the php server  in the rasa-router directory

```
cd rasa-router
php -S localhost:8000
```

## Connect to your chatwoot webwidget and start a conversation. 

if you are on your local machine, you can access the widget through the test page

```
http://localhost:3000/widget_tests
```

You can build on top of the ideas discussed here to implement your solutions. Refer to the [chatwoot api](https://www.chatwoot.com/developers/api/) to see the available options in chatwoot for your bots.Pretty excited to see what you guys come up with. 
