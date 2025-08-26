---
layout: single
title: "Playerbots"
permalink: /projects/playerbots/
author_profile: true
---

{% include base_path %}

## Playerbots & AI-Powered Game Characters

A (not so) short write-up on my recent investigation into Playerbots.

### Background

In my latest work examining how generative AI might be used in digital games, I stumbled upon a familar yet unexpected game which claimed to already have AI-powered game characters 
which promised to be highly immersive, capable of displaying personality, and would be near-indistinguishable from a human player. That game is World of Warcraft.

I have many years of experience with the game, first playing in 2008 and on and off for years following. World of Warcraft is a Massively Multiplayer Online Game (MMO),
meaning that thousands of players are online simultaneously, each pursuing their own in-game goals while occasionally partnering up with other players to complete more challenging content.
World of Warcraft has a fascinating history of use in academic writing, from Ge Jin's [Chinese Gold Farmers in the Game World](https://csrn.camden.rutgers.edu/newsletters/7-2/jin.htm)
to the [Corrupted Blood virtual pandemic incident](https://www.researchgate.net/publication/274073459_On_the_Problem_of_Predicting_Real_World_Characteristics_from_Virtual_Worlds).
Due to the game's large and persistent community of players, the game has often given rise to curious emergent social behaviours and interactions with real-world implications.
It is for this reason that I was surprised to see the game now being used to test out AI-Player interactions. I will detail how this has been happening in the following sections.

### Botting & Private Servers

"Botting" is a practice in which players use programs and scripts to automate their characters. This allows player characters to continue playing without any player input,
often to complete tedious tasks such as gathering resources or repeatidly killing the same enemy for virtual currency. Botting is also a bannable offense in World of Warcraft,
as it violates the game's Terms & Conditions and is widely considered to be a method of cheating. Nevertheless, due to the real-world value of the game's virtual currency,
players continue to employ bots to run their characters. 
More on this practice can be read from the numerous publications about developers [mass-banning bot accounts](https://www.thegamer.com/blizzard-banned-74000-bots-world-of-warcraft-classic-future-change/). 
While most World of Warcraft players believe bots to be either a nuscence or an outright game-ruining exploit, for the purposes of this exploration into AI-powered game characters, 
these bots represent an early glimpse into AI-Player interaction, and is overall viewed quite negatively given the context.

Another phenomenon relavent to this research is the propagation of private servers. Another highly bannable, if not often illegal, practice of running an emulated copy of World of Warcraft
is almost as old as botting. Through advanced server tools and C++ coding, it is possible to generate a fake game server hosted from the user's own computer. When the user logs into the game,
they don't log into one of World of Warcraft's servers, they instead log onto their own private server. These private servers can then be made publicly available (that's the illegal part), allowing other users
to log into them. A sort of "black market" network of private servers have developed parallel to the original game, and despite the game developer's past efforts to [shut them down](https://arstechnica.com/gaming/2016/04/blizzard-shuts-down-popular-fan-run-pirate-server-for-classic-wow/),
they too continue to run every day. While the first iterations of private servers originally sought to replicate the World of Warcraft experience as accurately as possible,
some of the latest big private server projects have been experimenting with custom content unique to their server, transforming the game World of Warcraft into something similar to a game engine.

As the private server community grew, so too did its ambitions and the robustness of its technology. 
Now most private servers are based on a single open-source distribution called [AzerothCore](https://www.azerothcore.org/). This software was designed to be highly modular, allowing community projects
to submit individual modifications (called modules in this context -- modding would be an appropriate term as well) to the code to implement specific features. These features can range from
gameplay improvements such as reduced character creation restrictions (making characters otherwise not possible in the original game) to entirely new game content such as custom maps.
One of the most popular modifications for this distribution is [Playerbots](https://www.azerothcore.org/catalogue.html#/details/646926161), which allows the server to populated with fake players
controlled by botting scripts.  

### What Playerbots Are

Playerbots make use of botting scripts to create and control up to 10,000 simultaneous player characters (it could likely go higher with sufficient computer memory). It begins by registering fake player
accounts in the server's database, then creates up to 10 in-game characters for each account. The playerbots are then able to login to all of their characters simultaneously and handle decision-making and actions for each character.
Playerbots operate using a simple decision tree based on in-game variables. If it has any quests, it will navigate towards them. If it's near a town, it will talk to the NPCs. If there are enemies
nearby, it will attack them. They are designed to mimic the actions and behaviour of real players, even going so far as to use the in-game chat to broadcast messages and talk to each other, form groups,
and even have pre-made strategies for handling combat and boss fights. It is worth noting that these Playerbots are not generative AI (but we'll get to that shortly), they are still simply running
scripts to handle repetitive in-game tasks and determine what they should do next.

There are two types of playerbots made available through these modules: randombots and altbots. 

Randombots are made to represent other players. They are generated when the server is launched and gradually populate the world. 
To avoid overloading the computer's memory, randombots are put to sleep whenever there is no nearby player (this functionality can be disabled but is not recommended). 
Randombots will otherwise function completely independent of real players and provide immersion through simulated player presence.
This is often desirable for private servers as their real player counts are often considerably lower than the original game, causing the large open world to feel emptier.
The addition of Randombots, particularly on individual (solo) private servers, allows players to play with and against other simulated players. 
In Player vs Player (PvP) encounters, players can team up with aligned Randombots to fight hostile Randombots, and bots aligned with the winning team in these matches also receive rewards.
Randombots are also capable of queueing up for PvP content, both starting and completing matches entirely without a human player's involvement.

Altbots, on the other hand, are made from the player's own characters. The player logs into the character of their choice and, through a simple in-game command, can generate a bot which logs in to one of their other characters. 
A player could then log out, log in to the other character, and generate a bot for their former character instead. 
Altbots offer an interesting opportunity of collaborative play with AI agents rather than competitive play. 
A player can't normally play two characters at once, as neither the game's systems nor the input requirements would cooperate with doing so, but with altbots, players can control multiples of their own characters at once.
Altbots don't act with nearly the same autonomy as randombots, as they are instead designed to follow player instructions. These instructions can be issued through chat messages or through the use of
in-game macros, which execute lines of text that can generate chat messages. A player can issue the command "attack my target" through either method, and all of the player's altbots will immediately
follow their instructions.

Altbots are capable of performing limited actions of their own accord, such as looting enemies or talking to NPCs, but will also run scripts to optimize their equipment,
sell unwanted items, and occassionally send messages to their player handler. Altbots provide a different sort of immersion to that of randombots. Where randombots help populate the world to appear more
active, altbots provide social immersion to the player in a similar style to having in-game friends or guildmembers. They accompany the player on their exploits and assist by progressing the player's other
characters for them. A player with 5 altbots levelling up with them would no longer need to level up each character individually, alleviating the need to repeat familiar quests, and ensuring the player always
has a team for completing more challenging content. In a sense, the use of altbots allows players to "play with (alongside) themselves."

There is a final type of Playerbot made available through this module called a "selfbot", which immediately transforms the player's own character into a bot while they are still using it. 
In my own tests of this functionality, selfbots cause a massive memory leak which crashes the game. It's unclear if this is simply a feature in development or an issue with my own setup.
Selfbots are, however, the least novel feature of the Playerbots module, as the functionality is identical to botting described in the previous section. Rather than allowing the player to play with or against
the AI, this simply has the AI play on behalf of the player.

### AI-Powered Playerbots

Now finally, we get to the AI integration. A seperate module called [Ollama Chat](https://www.azerothcore.org/catalogue.html#/details/954883822) connects all playerbots to a locally-hosted generative AI
through Ollama. While Ollama is designed to host AI servers in such a way that reduces their performance impact, all locally hosted generative AI utilize the computer's processing power to create their response.
As a result, connecting a large number of playerbots to Ollama has a significant impact on performance and hardware demand. The module is still in early development and can be a bit unstable given the
environment it's running in. Currently, its functionality is simple. Whenever a playerbot detects a message, it will send a prompt alongside of any relevant in-game variables to the Ollama-hosted LLM,
and after a few moments, will respond in-game. This furthers the illusion of playerbots mimicking human players, by allowing them to respond to messages as if they were one themselves.

Below I've included a chatlog from one such interaction between my own player character and two playerbots:  
Bob -- a human rogue, altbot  
Brendim -- a dwarf rogue, randombot  
 

| id | Player Name | Bot Name | Player Message                                           | Bot Reply                                                                 |
|----|-------------|----------|----------------------------------------------------------|---------------------------------------------------------------------------|
| 1  | JCoops      | Brendim  | That one is wearing a skull!                             | Aye, I see 'im alright, Jcoops. But I'm more interested in smashin' faces than skulls, mate. |
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
in-game variables, might react, I decided to increase the likelihood of input loop occurance. Also worth mentioning is that these logs only included details from the conversation between nearby bots,
while other bots were generating their own messages between each other elsewhere.

There are additional modules currently under development (unfortunately too experimental for my hardware to handle), which furthers playerbot integration with Ollama by referring to it during the decsion-making process.
Rather than consulting its own decision tree, these modules allow playerbots to prompt Ollama's connected LLM to suggest what action it undertakes next. While default playerbots' decision making isn't context-sensitive,
LLM-powered playerbots have a vastly larger source of knowledge and can advise playerbots on specific decisions to undertake. For example, while a playerbot is dependent solely on completing quests and killing enemies
to level up, the LLM might inform the playerbot of the best location to do this for its level, suggest specific quests to complete, and even pursue specific rewards. As similar modules continue to develop
and reinforce the integration between playerbots and LLMs, playerbots have the potential to take on increasingly human-like player qualities. With experimental features for playerbot personalities, including in-game trolling,
it's conceivable that at a certain point, it might become difficult to tell whether another player is in-fact another human.

### Playerbots and AI Futures

While I focused primarily on Playerbots as found on World of Warcraft private servers, I do want to emphasize that these are not the only Playerbots that have been developed for popular games (only the most familiar for me).
Minecraft has a host of different Playerbots applications, from [MinePal](https://minepal.net/) to Caltech's [Voyager Project](https://voyager.minedojo.org/).
Bethesda's The Elder Scrolls 5: Skyrim, one of the most popularly modded games ever, also has experimental LLM integration mods in the works, such as [Mantella](https://www.nexusmods.com/skyrimspecialedition/mods/98631?tab=posts),
a mod which is also available in Bethesda's [Fallout 4](https://www.nexusmods.com/fallout4/mods/79747).

This marks an interesting case of community-driven AI integration projects occuring within games that are owned by Microsoft. World of Warcraft is owned by Blizzard-Activision, a Microsoft acquisition
in 2023. Bethesda was acquired by Microsoft in 2021, only 2 years earlier. And Minecraft is also owned by Microsoft, purchased back in 2014. Microsoft owns several games on the bleeding edge of AI integration
using solutions such as Playerbots, but these endeavours are noticably not being led by Microsoft themselves.

Like most major technology companies, Microsoft is investing heavily in AI research, including for digital games through their [Game Intelligence Research Lab](https://www.microsoft.com/en-us/research/group/game-intelligence/).
However, their research focus currently appears to be on AI ideation: generating game visuals using AI for the purposes of digital prototyping. 
While this [Muse project](https://www.microsoft.com/en-us/research/blog/introducing-muse-our-first-generative-ai-model-designed-for-gameplay-ideation/) certainly has strong potential for aiding in designing
future AI-powered games, it doesn't fully take advantage of the numerous community-driven AI projects that are emerging from their own intellictual properties.

This potential clash between corporate priority and community development paves an interesting path forward for AI in games. Given Microsoft's ownership of the communities where these developments are occurring,
does this place Microsoft in a favourable position for future work with AI-driven game characters? Or does Microsoft's ownership present a risk to these communities by either siphoning their work or
shutting them down outright (particularly in legally-grey contexts such as private servers)?

While community-driven efforts will likely continue and expand across more games, these early traces of AI-driven game characters help identify potential future directions in which they might be taken.
Given their use in multiplayer games to create playerbots and singleplayer games to create more intelligent NPCs, there is a clear demand and use case for AI in these games: increased player immersion.

In this article I've highlighted several areas and instances in which playerbots can increase player immersion in games, from presence to cooperation, and using methods such as mimicking player behaviour
and engaging with in-game systems. This marks a stark contrast in how AI-powered NPCs achieve similar results, as they are often required to behave as if they belong to the game world they occupy
rather than actively engaging with it. While a playerbot would be considered immersive if it could take on in-game challenges such as defeating bosses, it would be highly immersion-breaking
for an in-game NPC to do the same. Imagine, if you will, a scenario in which the player attempts to take on the final boss of a game, only for a shopkeeper from the first act to beat them to it (as the credits begin to roll).

Ultimately, game developers, community project developers, technology companies, and players themselves will each have a hand in deciding when it is most appropriate for an AI-powered game character to
behave like a player (playerbots) or behave like an in-game character (NPC). There is still much work that can be done on identifying the characteristics and limitations of the two.

### Conclusion

Generative AI-powered videogame NPCs appear to be a goal for numerous game development studios, and while they struggle with design and implementation, community-driven efforts such as World of Warcraft playerbots
represent an untapped knowledge source for how AI might be integrated into future games. An unfortunate difficulty in accessing this knowledge source, however, is that it is built upon
proprietary code owned by a subsidiary of Microsoft and with a history of protecting its copyrighted material. For this reason, I can't include any screenshots or distribute the project files in any form,
lest I risk the wrath of copyright infringement. Nevertheless, strictly for research purposes, this environment does prove useful for further study on AI-Player interactions in games,
and a possible path forward for cooperation rather than competition between them.