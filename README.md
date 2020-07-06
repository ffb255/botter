<div align="center"><img src="https://raw.githubusercontent.com/ffb255/botter/master/resources/github/logo.png"></div>

![Packagist](https://img.shields.io/packagist/l/ffb255/botter)
![Packagist Version](https://img.shields.io/packagist/v/ffb255/botter)
![GitHub issues](https://img.shields.io/github/issues/ffb255/botter)

Botter is a PHP library, designed to build powerful [Telegram](https://telegram.org) bots in the fastest and easiest way possible.
```php
require_once "vendor/autoload.php";

use ffb255\Botter\BotterFactory;
use ffb255\Botter\Updates\Events\On;

$config = [
     'token' => "YOUR_BOT_TOKEN"
];
$botter = BotterFactory::create($config);

On::text("/start", function() use ($botter) {
    $botter->reply("Hello user!");
});

$botter->listen();
```

## Features
* Conversations
* Custom Request Builder
* Multi Level Cache Storage (Redis, JsonFile and etc..)
* Readable Codes
* Incoming update AutoComplete in IDEs (Full OOP)
![alt text][autocomplete]

## Installation
##### Using [Composer](https://getcomposer.org/):
```
composer require ffb255/botter
```

## Documentation
Check **[Wiki Pages](https://github.com/ffb255/Botter/wiki)** for documentation.<br>
You can find Botter methods with their examples in wiki.<br>

## Conversation
When it comes to chatbots, you probably don't want to react to single keywords, but instead, you might need to gather information from the user, using a conversation. Let's say that you want your chatbot to provide a rich user onboarding experience for your application users. In the onboarding process, we are going to ask the user for their first name and email address - that's a perfect fit for conversations! ([More on Conversation Wiki](https://github.com/ffb255/botter/wiki/Conversations))
<div align="center"><img src="http://up.vbiran.ir/uploads/2545115778763158723_conv-shot2.png"></div>

```php
$config = [
     'token' => "YOUR_BOT_TOKEN"
];
$botter = BotterFactory::create($config);

class SignupConversation extends Conversation {
     public function start()
     {
          $this->say("Welcome, Whats your name?");
          $this->next("askEmail");
     }

     public function askEmail()
     {
          $this->name = $this->getAnswer()->getText();
          $this->say("Whats your email?");
          $this->next("finishSignup");
     }

     public function finishSignup()
     {
          $name = $this->name;
          $this->say("Thanks {$name}! Your account has been created.");
          $this->finish();
     }
}

On::text("/signup", function() use($botter){
     $botter->startConversation(new SignupConversation);
});

$botter->listen();
```

## Why did I make Botter?
The goal was to simplify the process of making Telegram bots for my projects. ~2 years after I built Botter, I decided to publish it as an Open Source library.<br> 
Of course, there are still some problems in Botter that I am constantly trying to fix them. If you find a problem, you can tell me in [Issues](https://github.com/ffb255/Botter/issues).

[autocomplete]: https://raw.githubusercontent.com/ffb255/botter/master/resources/github/auto-complete-preview.png "Incoming Update Auto Complete"
[logo]: https://raw.githubusercontent.com/ffb255/botter/master/resources/github/logo.png "Botter Logo"

## License
Botter is free software distributed under the terms of the MIT license.
