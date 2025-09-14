---
layout: single
title: "Playerbots & AI-Powered Game Characters"
permalink: /projects/playerbots/
author_profile: true
---

{% include base_path %}

## Playerbots & AI-Powered Game Characters

A short write-up on my recent investigation into AI-powered NPCs called "Playerbots".

### Background

In my latest work examining how generative AI might be used in digital games, I stumbled upon a familiar yet unexpected game which already appeared to have working AI-powered game characters. 
These characters were presented as being highly immersive, capable of displaying personality, and would be near-indistinguishable from a human player. 
The game in question is World of Warcraft, but with some interesting caveats which I will present in this article.

I have many years of experience with this game, first playing in 2008 and on and off for years afterwards. World of Warcraft is a Massively Multiplayer Online Roleplaying Game (MMORPG),
meaning thousands of players are online simultaneously, each pursuing their own in-game goals while occasionally partnering up with other players to complete more challenging content.
World of Warcraft has a fascinating history of use in academic writing, from Ge Jin's [Chinese Gold Farmers in the Game World](https://csrn.camden.rutgers.edu/newsletters/7-2/jin.htm)
to the [Corrupted Blood virtual pandemic incident](https://www.researchgate.net/publication/274073459_On_the_Problem_of_Predicting_Real_World_Characteristics_from_Virtual_Worlds).
Due to the game's large and persistent community of players, the game has often given rise to curious emergent social behaviours and interactions, some with real-world implications such as the two linked above.
It is for this reason that I was surprised to see the game now being used to test out AI-Player interactions, but even more surprising still is that the developers themselves have seemingly little involvement in this.
In fact, the AI work occurring in this game actually runs counter to the developer's wishes and stem entirely from community-run efforts in ways that are often either against the game's Terms & Conditions or potentially even illegal.

### Botting & Private Servers

To examine the AI-Powered game characters used in World of Warcraft, there are two practices that must be examined: the use of bots and the propagation of private servers.  

"Botting" is a practice in which players use programs and scripts to automate their game characters. This allows player characters to continue playing without any player input,
often to complete tedious tasks such as gathering resources or repeatedly fighting the same enemies for virtual currency. 
The use of external scripts to automate gameplay is also a bannable offense in World of Warcraft, as it violates the game's Terms & Conditions, and is considered as cheating amongst the majority of the game's community.
Nevertheless, due to the real-world value of the game's virtual currency (see the above Gold Farming article for more information), it is not unusual to routinely encounter bots while playing the game. 
More on this practice can be read from the numerous publications about developers [mass-banning bot accounts](https://www.thegamer.com/blizzard-banned-74000-bots-world-of-warcraft-classic-future-change/). 
While most World of Warcraft players believe bots to be either a nuisance or an outright game-ruining exploit, for the purposes of this exploration into AI-powered game characters, 
these bots represent an early glimpse into AI-Player interaction, and is overall viewed quite negatively given the context.

The propagation of private servers represents the other relevant practice to the development of AI-Powered game characters. A private server is an emulated copy of the game's official servers,
created using advanced networking and C++ coding tools, which allows an individual copy of the game to redirect its connection towards the emulated server. In a sense, it allows a user to log in to their own
"private" copy of the game. These servers can then be hosted online, allowing other users to modify their game to connect to them.
Private servers are similarly a breach of the company's Terms and Conditions just for accessing them, and quickly become legal issues over distribution and operation.
Distribution of private servers is tantamount to online piracy, and hosting the servers opens up numerous copyright violations, especially when the server is monetized (as many private servers are).
Major lawsuits have occurred between private server hosts and Blizzard-Activision, as recently as [last week](https://www.gamespot.com/articles/wow-most-ambitious-private-server-is-being-sued-by-blizzard/1100-6534413/),
but despite the considerable risk of shutdown and reprisal, private servers are more popular than ever, with over 100,000 users presently subscribed to the r/WoWServers subreddit alone.

A sort of "underground" network of private servers have developed parallel to the original game, with the earliest iterations seeking to accurately replicate the World of Warcraft experience,
now some of the latest big private server projects have been experimenting with custom content unique to their server, transforming the game World of Warcraft into something similar to a game engine. 
Many private servers are based on an open-source distribution called [AzerothCore](https://www.azerothcore.org/). This distribution was designed to be highly modular, allowing community projects
to submit individual modifications (called modules in this context -- "modding" would also be an appropriate term) to the code, allowing users to pick and choose specific features to implement. 
These features can range from gameplay improvements such as reduced character creation restrictions (making characters otherwise not possible in the original game) to entirely new game content such as custom maps.
One of the most popular modifications for this distribution is [Playerbots](https://www.azerothcore.org/catalogue.html#/details/646926161), which allows the server to be populated with fake players
controlled by botting scripts. 

For the purpose of investigating Playerbots, I was able to create my own standalone build of the distribution under legal fair use and AGPL 3.0 licensing.
To avoid risking the wrath of copyright infringement claims, none of the code is publicly available nor will any screenshots including copyrighted material be presented.
This article is in no way advocating for digital piracy and the intention is to compile the information as thoroughly as possible so no one else need do so themselves.

### What Playerbots Are

Playerbots make use of botting scripts to create and control up to 10,000 simultaneous player characters, which could likely go higher with sufficient computer memory. 
It begins by registering fake player accounts in the server's database, then creates up to 10 in-game characters for each account. 
The playerbots are then able to login to all of their characters simultaneously and handle decision-making and actions for each character.
Playerbots operate using a simple decision tree based on in-game variables. If it has any quests, it will navigate towards them. If it's near a town, it will talk to the NPCs. If there are enemies
nearby, it will attack them. They are designed to mimic the actions and behaviours of real players, even going so far as to use the in-game chat to broadcast messages and talk to each other, form groups,
and even have pre-made strategies for handling combat and boss fights. It is worth noting that these Playerbots are not generative AI (but we'll get to that shortly), they are still simply running
scripts to handle repetitive in-game tasks and determine what they should do next.

There are two main types of playerbots made available through these modules: randombots and altbots. 

Randombots are made to represent other players. They are generated when the server is launched and gradually populate the world. 
To avoid overloading the computer's memory, randombots are put to sleep whenever there is no nearby player (this functionality can be disabled but is not recommended). 
Randombots will otherwise function completely independent of real players and provide immersion through simulated player presence.
This is often desirable for private servers as their real player counts are often considerably lower than the original game, causing the large open world to feel emptier.
The addition of Randombots, particularly on individual (solo) private servers, allows players to play with and against other simulated players. 
In Player vs Player (PvP) encounters, players can team up with aligned Randombots to fight hostile Randombots, and bots aligned with the winning team in these matches also receive rewards.
Randombots are also capable of queueing up for PvP content, both starting and completing matches entirely without a human player's involvement.

Altbots, on the other hand, are made from the player's own characters. The player logs into the character of their choice and, through a simple in-game command, can generate a bot which logs in to one of their other characters. 
A player could then log out, log in to their other character, and generate a bot for their former character instead. 
Altbots offer an interesting opportunity of collaborative play with AI agents rather than competitive play. 
A player can't normally play two characters at once, as neither the game's systems nor the input requirements would cooperate with doing so, but with altbots, players can control up to 40 of their own characters simultaneously.
Altbots don't act with nearly the same autonomy as randombots, as they are instead designed to follow player instructions. These instructions can be issued through chat messages or through the use of
in-game macros, which execute lines of text that can generate chat messages. A player can issue the command "attack my target" through either method, and all of the player's altbots will immediately
follow engage in combat.

Altbots are also capable of performing limited actions on their own, such as looting enemies or talking to NPCs, but will also run scripts to optimize their equipment,
sell unwanted items, and occasionally send messages to their player handler. Altbots provide a different sort of immersion to that of randombots. Where randombots help populate the world to appear more
active, altbots provide social immersion to the player in a similar style to having in-game friends or guild members. They accompany the player on their exploits and assist by progressing the player's other
characters for them. A player with 10 altbots would no longer need to level up each character individually, alleviating the need to repeat familiar quests and ensuring the player always
has a group for completing more challenging content. In a sense, the use of altbots allows players to "play with (alongside) themselves."

There is a final type of Playerbot made available through this module called a "selfbot", which immediately transforms the player's own character into a bot while they are still using it. 
In my own tests of this functionality, selfbots cause a massive memory leak which crashes the game. It's unclear if this is simply a feature in development or an issue with my own setup.
Selfbots are, however, the least novel feature of the Playerbots module, as the functionality is identical to botting described in the previous section. Rather than allowing the player to play with or against
the AI, this simply has the AI play on behalf of the player.

### AI-Powered Playerbots

Now we get to the AI integration portion of this investigation. 
An Azerothcore module called [Ollama Chat](https://www.azerothcore.org/catalogue.html#/details/954883822) allows all playerbots to connect to a locally-hosted generative AI
through a software called [Ollama](https://ollama.com/). While Ollama is designed to host AI servers in such a way that reduces their performance impact, all locally hosted generative AI utilize the computer's processing power to create their response.
As a result, connecting a large number of playerbots to Ollama has a significant impact on performance and hardware demand. The module is still in early development and can be a bit unstable given the
environment it's running in. Currently, its functionality is rather simple: whenever a playerbot detects an in-game chat message, it will send a prompt alongside of any relevant in-game variables to the Ollama-hosted LLM,
and after a few moments, will respond in-game. This furthers the illusion of playerbots mimicking human players, by allowing them to respond to messages as though they were human players too.

Below I've included a chatlog from one such interaction between my own player character and two playerbots:  
Bob -- a human rogue, altbot  
Brendim -- a dwarf warrior, randombot  
 

| id | Player Name | Bot Name | Player Message                                           | Bot Reply                                                                 |
|----|-------------|----------|----------------------------------------------------------|---------------------------------------------------------------------------|
| 1  | JCoops      | Brendim  | That monster is wearing a skull!                         | Aye, I see 'im alright, Jcoops. But I'm more interested in smashin' faces than skulls, mate. |
| 2  | JCoops      | Brendim  | How close are you to levelling up?                       | Aye, not far off now, Jcoops. Keep the demons at bay till I get there!    |
| 3  | JCoops      | Brendim  | How's everyone doing?                                    | Aye, Brendim here, smashin' skulls as usual in Northshire Valley, ye? Watch yer back out there, Jcoops! |
| 4  | Bob         | Brendim  | Stealthin' and stabbin', just the usual here, Jcoops.    | Bob, keep stealthin', but watch yer back, mate! I'm here in Northshire, ready to take on challenges together. |
| 5  | Bob         | Brendim  | Aye Brendim, I'm just lurkin' around the shadows waitin' for an opportunity to strike. | Noted, Bob. Time to step out from the shadows, eh? Let's see how you fare against this here axe. |
| 6  | Bob         | Brendim  | Alright Brendim, time to dance. Shadows first, axe second. | Alright Bob, let's not forget I'm the tank here, shield up when we dance. |
| 7  | JCoops      | Bob      | Quit arguing you two!                                    | Quieting down, Jcoops? Just a bit more practice in the art of stealth, and you'll have 'em whispering our name instead. |
| 8  | Brendim     | Bob      | Noted, Bob. Time to step out from the shadows, eh? Let's see how you fare against this here axe. | Alright Brendim, time to dance. Shadows first, axe second. |
| 9  | Brendim     | Bob      | Alright Bob, let's not forget I'm the tank here, shield up when we dance. | Got it, boss. Stay close and watch my back, shield up when I dance.       |

Worth noting is that both playerbots input and respond to player messages, but also to each other, creating an amusing loop in which the playerbots began to respond to each other's responses towards me.
Input loops like this can be modified by reducing the likelihood of bots responding to other bots, but for the sake of witnessing how two playerbots, both connected to a generative AI and with different
in-game variables, might react, I decided to increase the likelihood of input loop occurrence. Also worth mentioning is that these logs only included details from the conversation between nearby bots,
while other bots were generating their own messages between each other elsewhere.

There are additional modules currently under development (unfortunately too experimental for my hardware to handle), which furthers playerbot integration with Ollama by referring to it during the decision-making process.
Rather than consulting its own decision tree, these modules allow playerbots to prompt Ollama's connected LLM to suggest what actions or activities it undertakes next. While default playerbots' decision making isn't context-sensitive,
LLM-powered playerbots have a much larger pool of knowledge and can advise playerbots on specific decisions to undertake. For example, while a playerbot is dependent solely on completing quests and fighting nearby enemies
to level up, the LLM might inform the playerbot of the best location to do this for its level, suggest specific quests to complete, and even pursue specific rewards. As similar modules continue to develop
and reinforce the integration between playerbots and LLMs, playerbots have the potential to take on increasingly human-like player qualities. With experimental features for playerbot personalities, including in-game trolling,
it's conceivable that at a certain point, it might become difficult to tell whether another player is in-fact another human.

### Playerbots and AI Futures

While I focused primarily on Playerbots as found on World of Warcraft private servers, I do want to emphasize that these are not the only Playerbots that have been developed for popular games (only the most familiar for me).
Minecraft has a host of different Playerbots applications, from [MinePal](https://minepal.net/) to Caltech's [Voyager Project](https://voyager.minedojo.org/).
Bethesda's The Elder Scrolls 5: Skyrim, one of the most popularly modded games ever, also has experimental LLM integration mods in the works, such as [Mantella](https://www.nexusmods.com/skyrimspecialedition/mods/98631?tab=posts),
a mod which is also available in Bethesda's [Fallout 4](https://www.nexusmods.com/fallout4/mods/79747).

This marks an interesting case of community-driven AI integration projects occuring within games that are owned by Microsoft. World of Warcraft is owned by Blizzard-Activision, a Microsoft acquisition
in 2023. Bethesda was acquired by Microsoft in 2021, only 2 years earlier. Minecraft is also owned by Microsoft, purchased back in 2014. Microsoft owns several games on the bleeding edge of AI integration
using solutions such as Playerbots, but these endeavours are noticably not being led by Microsoft themselves, and in the case of World of Warcraft, is actively being hampered by developers through lawsuits over copyright issues.

Like most major technology companies, Microsoft is investing heavily in AI research, including for digital games through their [Game Intelligence Research Lab](https://www.microsoft.com/en-us/research/group/game-intelligence/).
However, their research focus currently appears to be on AI ideation: generating game visuals using AI for the purposes of digital prototyping. 
While this [Muse project](https://www.microsoft.com/en-us/research/blog/introducing-muse-our-first-generative-ai-model-designed-for-gameplay-ideation/) certainly has strong potential for aiding in designing
future AI-powered games, it doesn't fully take advantage of the numerous community-driven AI projects that are emerging from their own intellictual properties.

This potential clash between corporate priority and community development paves an interesting path forward for AI in games. Given Microsoft's ownership of the communities where these developments are occurring,
does this place Microsoft in a favourable position for future work with AI-driven game characters? Or does Microsoft's ownership present a risk to these communities by either siphoning their work or
shutting them down outright (particularly in contexts such as private servers)?

While community-driven efforts will likely continue and expand across more games, these early traces of AI-driven game characters help identify potential future directions in which they might be taken.
Given their use in multiplayer games to create playerbots and singleplayer games to create more intelligent NPCs, there is a clear demand and use case for AI in these games, mainly increased player immersion.

In this article I've highlighted several areas and instances in which playerbots can increase player immersion in games, from presence to cooperation, and using methods such as mimicking player behaviour
and engaging with in-game systems. This marks a stark contrast in how AI-powered NPCs achieve similar results, as they are often required to behave as if they belong to the game world they occupy
rather than actively engaging with it. While a playerbot would be considered immersive if it could take on in-game challenges such as defeating bosses, it would be highly immersion-breaking
for an in-game NPC to do the same. Imagine, if you will, a scenario in which the player attempts to take on the final boss of a game, only for a shopkeeper from the first act to beat them to it (as the credits begin to roll).

Ultimately, game developers, community project developers, technology companies, and players themselves will each have a hand in deciding when it is most appropriate for an AI-powered game character to
behave like a player (playerbots) or behave like an in-game character (NPC). There is still much work that can be done on identifying the characteristics and limitations of the two.

### Conclusion

Generative AI-powered videogame NPCs appear to be a goal for numerous game development studios, and while they continue to work on different designs and implementations, 
community-driven efforts such as World of Warcraft playerbots presents an untapped knowledge source for how AI might be integrated into future games. 
These cases represent how users themselves want to engage with AI in gaming contexts, and as such, they demonstrate a trend towards cooperative play alongside of AI agents rather than forced
competition against them. Observing how game modding communities, both legal and otherwise, continue to implement AI-powered game characters in the future promises a potentially more realistic
depiction of their long-term adoption in these spaces. While Playerbots themselves are only one such implementation, I look forward to keeping track of other new and exciting developments!