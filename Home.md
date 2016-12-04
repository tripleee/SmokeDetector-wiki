SmokeDetector is a headless chatbot that detects spam and posts it to chatrooms.  
It uses [ChatExchange](https://github.com/Manishearth/ChatExchange) and takes questions from [the Stack Exchange realtime tab](http://stackexchange.com/questions?tab=realtime). For more information on how it works, see our website at [charcoal-se.org](http://charcoal-se.org/).

***

###User information

 - You can find a list of **SmokeDetector's commands** on [the Commands wiki page](https://github.com/Charcoal-SE/SmokeDetector/wiki/Commands).

 - Find a list of **chatrooms that SmokeDetector interacts with** on [the Chat Rooms wiki page](https://github.com/Charcoal-SE/SmokeDetector/wiki/Chat-Rooms).

 - If you're thinking about **asking for privileges**, take a look at the [Privileges](https://github.com/Charcoal-SE/SmokeDetector/wiki/Privileges) page.

 - If you're looking for **guidance on feeding back to SmokeDetector**, read [Feedback Guidance](https://github.com/Charcoal-SE/SmokeDetector/wiki/Feedback-Guidance).

###Developer information

 - For information on **how to write a new check for spam**, see [Docs: Creating new spam checks](https://github.com/Charcoal-SE/SmokeDetector/wiki/Docs:-Creating-new-spam-checks).

 - If you wish to **integrate with Smokey** and Metasmoke via our API, see the [API Docs](https://github.com/Charcoal-SE/metasmoke/wiki/API-Documentation).

***
###Glossary:

- **Blacklist** - list of users whose every question or answer will be posted to the appropriate chatrooms. This should be used **only for spammers or** for users whose posts merit **abusive/offensive flags.**

- **Whitelist** - list of users which are free from username checks on their posts. Title and body will still be checked.