=== Plugin Name ===
Contributors: webxid
Donate link: https://bit.ly/3JSMitJ
Tags: telegram, bot, responder, messaging, mailing, chatbot, chat-bot, chat
Requires at least: 4.9
Tested up to: 6.0.2
Stable tag: 1.0.1
Requires PHP: 7.2
License: Apache 2.0
License URI: http://www.apache.org/licenses/LICENSE-2.0

The plugin helps to send a message to a Telegram Bot subscribers

== Description ==

GitHub project: [https://github.com/bots-master/wp-bots-master](https://github.com/bots-master/wp-bots-master)

**The features list**
- Telegram Bot integration
- Send a message to all Telegram Bot's Subscribers
- Send a message to Telegram Group Chat
- Post a message in Telegram Channel

**Requirements**

PHP version 7.2 or later


== Installation ==

1. Download and unzip the plugin into `/wp-content/plugins/` directory
2. Activate the plugin in your wordpress admin panel
3. Go to `Bot Master > Bot Settings` page
4. Set your Telegram Bot API Token

Done!

== Uninstall The Plugin ==

To uninstall the plugin permanently, follow the next steps:
1. Drop the DB table *wx_bot_users*:

SQL Query: `DROP TABLE IF EXISTS wx_bot_users;`

2. Remove WP Options:

`delete_option('telegram_api_token');
delete_option('welcome_message');
delete_option('unknown_message');`

Done! Now, there is no data of the plugin in DB

== How To Use ==

### Collect Subscribers

!!! IMPORTANT !!!
If a user was subscribed to a bot before the bot installing, it will not works.
The plugin does not able to grab your bot's old subscribers from the Telegram side.

So, you are able to message users after the next steps
1. Set a Telegram Bot API Token in WP Admin
2. A user subscribe to the bot (send any message or click any button)

Now, you are able to message the subscriber.


### Group Chat / Channel

**Add Group Chat / Channel to The Chatbot**

1. Go to the Telegram and create public a Group Chat or a Channel (Chat)
2. Add your Bot to the Chat. It has to be able to post a message.
3. Copy the Chat `username`
4. Go to `Bot Master > Channels` and add the username here

Now, your bot will posts a message to the Chat, you send at `Bot Master > Send Message`


== Code Usage ==

`use WebXID\BotsMaster\ChatBot;
use WebXID\BotsMaster\ChatBot\BotUser;

BotUser::find(['type_id' => ChatBot\BotUser::TYPE_CHAT]); // returns all Group Chats and Channels list
BotUser::find(['type_id' => ChatBot\BotUser::TYPE_USER]); // returns all subscribers

BotUser::all(); // returns all records

// -------------------------

$bot_user = BotUser::findOne(['type_id' => ChatBot\BotUser::TYPE_USER]);

if ($bot_user) {
    ChatBot::factory($bot_user)
        ->sendMessage('<b>Hello</b> world!'); // will send the message, if the plugin installed correctly
}`

Please, check the Doc [https://core.telegram.org/bots/api#html-style](https://core.telegram.org/bots/api#html-style) to get allowed HTML tags


== Screenshots ==

1. `Bot Master > Bot Settings` page
2. `Bot Master > Channels` page
3. `Bot Master > Send Message` page


== Changelog ==

= 1.0.1 =
* The last WP version Checked
* Removed uninstall logic - so, if you deactivate then activate the plugin, the all data will be available as before the deactivation

= 1.0 =
* Initial
