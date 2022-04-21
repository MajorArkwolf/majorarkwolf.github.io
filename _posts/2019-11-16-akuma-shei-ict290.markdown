---
layout: post
title:  "Akuma Shei"
date:   2019-11-16 12:00:00 +0800
categories: University
---
## Roguelike / Nethack
### ICT290 University Project

This project was probably the highlight of 2019 for myself. Prior to the commencement of this unit, I had already picked out my group. We were a fierce machine of coders ready to take on the monolith that was Shay’s world. For those who do not know, Shay’s world is almost a 1:1 scale of Bush Court, Murdoch created by an ex-student of Murdoch. Shay had little to no C++ coding experience before making this game and hats off to him for trying his best. There were also a few “questionable” syntax errors in the codebase that my group is adamant were added later by the tutors to add more challenge into getting this code to work.

#### Part One

So, we set out on the quest to get Shay’s World running and then adding our own game to this world. We broke this project up into two parts to reflect the Assignment criteria. Part 1 was simple, get it running and model a new area of the map. As a group, we chose to build the Murdoch Tavern which is where we ran into issue one… complex shapes. Most of us had basic experience with primitive squares, circles and triangles; however, the Tavern has a bunch of curved walls and strange surfaces and we had no idea how to tackle this problem using primitives effectively. That is when we decided we would build our own OBJ/MTL loader. I was tasked with building the Tavern in Maya and exporting it while also adding a new staircase to the world and fixing some unoptimized code. One of the unoptimized code segments I had to fix was when I discovered that a linked list was being used as an array and was being iterated through in an incredibly inefficient manner. Since the list was encapsulated (Thank you so much, Shay, for this), I was able to gut it and swap it for an STL vector, which saw a small performance increase.

[Click here to view part 1](https://www.youtube.com/watch?v=RqZ-s336jR8).
#### Part Two

So, part two is when our group had to go into overdrive. During part one, we had to discuss and design the ideas of our game. Originally, I wanted to do a puzzle-platformer due to simplicity; however, my group didn’t want such a simple task and I am glad they talked me out of the idea. A member dropped the idea of Nethack RPG, and then next minute, we are writing out all these ideas. I was tasked with making the game logic and modifying the asset to be passed into our OBJ loader. We had also discussed early on that animation would be an enormous hurdle and opted to make an artistic choice, treat the models like chest pieces. So I began posing and then converting the models from quads to triangles. After this was done I worked on building a Hybrid Entity Component System, also known as a HECS. I am so glad I opted for an ECS system over an inheritance-based system as it worked flawlessly.

[Click here to view part 2](https://www.youtube.com/watch?v=dQjQ6_uyiwo).

Overall I enjoyed this project a lot and the experience I learned from resources and group members will pay off later in life.
