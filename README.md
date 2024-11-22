# Sindarin's Portfolio

This repository contains the source material for [my portfolio website](https://www.sindarin27.net). 

A rough draft of the things that will be shown and discussed in the portfolio is shown in the draft section of this document. It might be desirable to add code examples?

## Drafts

### Applying Volumetric Sampling Methods to the Rendering of Rain Droplets (2024)
![Amazon Bistro scene displaying rain](amazon-bistro-rain.png)
I developed a new technique for rendering physically accurate rain streaks for my master thesis and implemented it in the rendering software [PBRT-4](https://www.pbrt.org/). 

Inspired by volumetric rendering techniques such as the one implemented in <a href="advancedgraphics.html">one of my previous projects</a>, I started researching the possibilities of using the same techniques to render rain streaks from a procedurally generated volume. In addition to researching more about existing volumetric rendering techniques, this included research into the physical properties of rain and the challenges these would present. I also implemented a ground truth algorithm to use for comparison with the method I was to develop.

The final implementation and math went smoothly and presented further optimisation possibilities by replacing the smallest rain drops with a uniform fog throughout the scene. The extra predictability presented by volume sampling allows a lot of noise reduction compared to the ground truth method, and allows the algorithm to run on the GPU. The method is still impractically slow for real-time rendering and requires further research to be fully physically accurate, but is currently one of the first approaches to rain rendering in the raytracing scene.

### Gaslit (2023)
![Screenshot of the game Gaslit. Tiles the player can place are shown in the bottom-left corner. A quest bubble is shown above one of the communities towards the bottom-right corner, displaying the requirements of the quest and the progress towards them. An LNG terminal is visible towards the middle-left, with a pipeline leading to a gas field.](gaslit-gameview.png)
At the request of Fossielvrij NL and in collaboration with a small team of artists and developers from the HKU Univeristy of Arts, I developed a casual game that introduces the player to the threat of the LNG industry to local communities. Time granted for this project was four months.

The player places tiles in the world to build a world, completing requests of communities scattered around the world by connecting landscapes of the same type. After some turns, an LNG terminal will appear and destroy part of the land. Gas fields will continue appearing and expanding, with pipelines connecting them to the terminals. This breaks up landscapes, which in turn makes quests harder to complete. The expansion of gas fields can also destroy communities, and if this happens too many times the player loses the game. The game has a scaling difficulty, such that the gas industry becomes more aggressive as more turns go by.

A Gaslit world is fully serializable and the player's progress is saved whenever they open the main menu, close the game, or when a set number of turns passes. All quests, upgrade tile locations, moves by the gas industry, and decorative objects use a seed randomly generated at the start of the game and saved to the file. To give a concrete example, this means the same community always has the same needs on the same save file — even if the community was not yet visible when the game last saved.

The game was developed in close collaboration with Fossielvrij NL by following Scrum guidelines, with a product increment delivered every two weeks to gather feedback and adjust our approach where necessary. 

This game can be played on https://fossielvrijnl.itch.io/gaslit.

![Screenshot of the game Gaslit, showing a quest panel](gaslit-questpanel.png)

Keywords: C#, Unity, Scrum, CI, Serious Games

### Raytracer from scratch (2023)

![House on top of a hot air balloon, surrounded by clouds.](agr_flying.png)

During the Advanced Graphics course, I developed a raytracer from scratch together with another student. The program can render scenes with different materials such as glass and mirrors, applied to different shapes such as spheres and triangles, and using different raytracing algorithms such as the Whitted algorithm and the Monte Carlo algorithm (and a number of debug algorithms). Creating an algorithm to build and use a BVH to speed up the rendering process was also part of the assignment.

After implementing the basic functionality for the raytracer and BVH, we added additional features such as loading 3D models from OBJ files, supporting textured models, implementing glossy materials, and implementing the process of BVH building on the GPU.

Finally, I implemented the paper "A null-scattering path integral formulation of light transport" by Miller *et al.* to render volumetric clouds in a scene, with the density of the cloud at a position determined using a custom cloud-generation algorithm developed by my teammate. In addition to the basic rendering of volumes using said technique, I also added support for next-event estimation within the volume.

With the many types of materials, shapes, and algorithms that all need to be swapped out depending on scene and user settings, the project required not only the math typical of rendering: proper code organisation was almost as important, and a lot of our effort went into keeping the program expandable to keep it easy to add new shapes, materials, and algorithms.

![Two robot characters from the game Portal floating in space, reflecting the light of a nearby nebula.](agr_Portal.png)

Keywords: C#, RTX, GPU, PBR

### Farsighted Mobs Rework (2024)
![An example of a rule supported by the reworked version of the mod: entities of the creeper type spawned when the weather is raining receive a 20% to their size and a 50% health bonus.](farsighted-rainy-creepers.png)
Farsighted Mobs is one of my Minecraft mods, popular with modpack developers (people compiling a selection of mods and configuration settings to create a unique play experience) for its ability to make the game significantly harder by allowing monsters to see the player from further away. The only functionality in the mod when I created it in 2020 were the option to increase the default "follow range" of monsters, as well as adding individual overrides for certain creatures. I desired more flexibility and control, which is why I decided to rework the mod in October 2024.

Minecraft includes a predicate system used to generate loot when a chest is opened or a creature is killed in the base game, and designed to be extremely flexible. By incorporating this predicate system to determine whether a creature should be affected by my mod, modpack developers are granted the same options, and any future predicates added to the base game will automatically be accessible to the mod. Any predicates added by other mods will also be available to users of my mod, and my mod includes a small number of predicates which can thus be used for loot generation too.

The game also uses an attribute system for creatures: each creature is assigned attributes for things such as follow range, health, size, et cetera. The original mod only affected the follow range to make mobs see the player from further away, but the same approach can be used to affect other attributes — including attributes added by other mods or introduced in future versions of the game.

The combination of these two features creates an extremely flexible and modular system. The default behaviour of the mod is only slightly changed: the distance monsters see players from now depends on the difficulty of the game. But the new configuration options allow for nearly anything, from spawning animals with less health on a player's first day to spawning larger monsters during a full moon.

### Side Tracked (2024)
![Cover image of the game Side Tracked, showing a wooden train on a rail and a small camp in the forest behind it.](SideTrackedCover.png)
Side Tracked is a small game about wooden trains, which I created during a single-weekend game jam. The game has the player dragging around a small train over a wooden train track, passing through a number of environments on their way. 

With the primary mechanic of the game being the dragging of the train along its rail, most of my effort was devoted to making this mechanic work smoothly and feel satisfying to the player. This included experimentation with the hitbox of the train (where should the player be able to click for the train to respond?), how fast the train should move, how far the mouse pointer could deviate from the track for the train to move, where the train should move if the player's mouse is not directly on the track, et cetera. Equally important was ensuring a smooth transition between tracks, and providing feedback to the user when the train could not move.

The game features a simple save system so a player can leave after completing a level or replay a level they have already completed. Although the project was created during a game jam, the code is modular enough that future levels could be added if I ever wish to continue development on the game.

Although the game was brought to a completed state for the game jam, there are still many levels I wished to add to the game but did not have time for, and the levels currently in the game function mostly as an introduction to mechanics I wished to use in more complicated puzzles. A single weekend is very little time to create a full game, it turns out! Nevertheless, I am very happy with the result, and the game was voted as winner of the game jam.

This game can be played on https://sindarin27.itch.io/side-tracked.

![A level of the Side Tracked game, showing a switch track. A yellow train is on one side of the switch, a blue train on the other. Behind the track is a play mat with a yellow car placed on a road.](SideTrackedLevel3.png)

Keywords: C#, Unity, Game jam, Web game

### A Song of Ice and Fire Roleplaying Tool (2024)
![A map of Westeros at the "duchy" level, as used by the tool. Each shade represents a different region.](westerosMap_duchies.png)
I developed an unofficial tool for the Song of Ice and Fire Roleplaying game with a small team of friends from a data science and economics background. This tool assists the game masters ("referees" running the game) with keeping a high-level overview of the game world, simulating things such as weather, food, and troop movement that would otherwise take a lot of manual work. The project was split into multiple modules that communicate through the file system. I worked on the modules for weather simulation and food production and consumption, a tool to convert maps to a format usable with the tool, as well as the central module that controls when the other modules should activate. Troop movement and the written specifications of each module were handled by the rest of the team. 

In case of both the weather and food modules, data management was the primary challenge. Data had to be stored in a format usable for all modules (for example, food production depends on the weather) as well as readable for the game masters (for example, the game master wants to tell a player how many weeks of food are in their castle), which is why the choice was made to use CSV files for all modules. Both modules used a central interface with functions for reading, updating, and writing the files available to the other modules, as well as a number of utility methods to handle their own internal logic to update the state of the world.

![A sample of code from the weather module. This function updates the dataframe containing dice rolls for weather, factoring in wind.](asoiaf_code_fragment.png)

To avoid the manual labor of drawing our own map or interpreting a map designed for humans rather than computers, I designed the map conversion tool to create and visualise a map from files present in the Crusader Kings 3 conversion mod "A Game of Thrones", set in the same world as the roleplaying game. This map contained nearly 7000 regions, far too much for our game, but also contained files describing a hierarchy of regions. My tool reads these files, traverses the hierarchy, and builds a new map at a scale with larger regions. My weather module additionally needed information about the borders between regions, so I added a step to the conversion program to detect all borders and their direction using a number of image processing techniques. These borders are written to an additional CSV file, allowing game masters to make the final call on borders: for example, a border might want to be removed due to a large mountain range separating the two regions physically.

![The original map of Westeros with many extremely small regions. Each shade represents a different region.](westerosMap_provinces.png)

The central module handles the communication between the game master and the other modules. This module makes calls to all other modules to update the state of the world based on input by the game masters. 

The tool was used live during a week-long game and the game masters considered the tool a great success, reducing their workload even further than the Excel sheets used in previous games and considering to automate even more parts of the game in the future.

Keywords: Python, Data management, Image processing

### Radio Marina (2024)

Preview: ![Image of the glitched page](radio-marina-glitched.png)

![Image of the normal Radio page](radio-marina-home.png)

When creating my character for an outdoor roleplaying event, I decided I wanted to play an anarchist running a pirate radio. The event already had participants playing music on their phones to simulate radio or record players, and I saw an opportunity to introduce live radio broadcasts. 

With the event being in the middle of a forest, connection was a major issue. I solved this using the hotspot functionality on a Raspberry Pi, creating a small local network. The range of this network was large enough to cover the most relevant playing area; outdoor conditions are good for connections, as is the lack of interference in such a location. The network can easily be expanded in the future using a more powerful WiFi router or a network of mobile phone hotspots if necessary.

![Photo of the event site before the game, taken while testing my setup. The Raspberry Pi is in the tent, while I'm standing at the maximum range for a reliable WiFi connection with the hotspot.](radio-onsite.jpg)

Also installed on the Raspberry Pi is the AzuraCast software, a flexible framework for running online radio. In my case, I used it to run two radio channels on separate web pages: one for my own radio channel and one to facilitate the event's own channel. 

When the Raspberry Pi is connected to the larger internet, traffic is routed from an address on my own website to the radio's web pages. When the device is offline, it runs its own DNS to point users to the same website. I initially considered simply using the IP address of the Raspberry Pi to connect to the radio, but this made browsers warn or even prevent users from using HTTPS when connected. This approach allows the device to stay offline for 90 days and still maintain a trusted certificate — more than long enough for my use case.

![Screenshot of the JavaScript code.](radio-marina-code-sample.png)

To add an additional "puzzle element" to the radio, I recently added a third, 'secret' radio channel filled with secret messages. Scattered throughout my character's belongings are calculations, blueprints, and wiring diagrams for running a radio channel encrypted within her normal radio channel. Specifically, some of the sounds are manipulated to cancel out when the sound waves are combined with that of another radio frequency, revealing a secret third channel. Do not ask me about the physical accuracy of this; I'm not a physicist and all of this is for a game of make-believe. Much more my thing is actually implementing this: AzuraCast provides the option to add your own JavaScript code to its web pages. By finding out which events AzuraCast uses to start and stop a stream and communicating this information across tabs, I was able to detect when a user started playing 2 different radio channels at the same time. When this happens, my code replaces the audio source of one of the streams with the audio source of the secret stream. To provide the person discovering this secret with visual feedback as well, the background and title of the page change to represent the glitched nature of the secret radio stream.

All in all, this project was a lot of fun to work on, and invited many other players to contribute to the radio in their own way — which is the ultimate reward for a project like this. 

![Image of the glitched page]()

Keywords: JavaScript, Web Development, Offline Communication