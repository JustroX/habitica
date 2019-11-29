Habitica ![Build Status](https://github.com/HabitRPG/habitica/workflows/Test/badge.svg) [![Code Climate](https://codeclimate.com/github/HabitRPG/habitrpg.svg)](https://codeclimate.com/github/HabitRPG/habitrpg) [![Bountysource](https://api.bountysource.com/badge/tracker?tracker_id=68393)](https://www.bountysource.com/trackers/68393-habitrpg?utm_source=68393&utm_medium=shield&utm_campaign=TRACKER_BADGE) [![Open Source Helpers](https://www.codetriage.com/habitrpg/habitica/badges/users.svg)](https://www.codetriage.com/habitrpg/habitica)
===============

[![Greenkeeper badge](https://badges.greenkeeper.io/HabitRPG/habitica.svg)](https://greenkeeper.io/)

[Habitica](https://habitica.com) is an open source habit building program which treats your life like a Role Playing Game. Level up as you succeed, lose HP as you fail, earn money to buy weapons and armor.

**We need more programmers!** Your assistance will be greatly appreciated. The wiki pages below and the additional pages they link to will tell you how to get started on contributing code and where you can go to seek further help or ask questions:
* [Guidance for Blacksmiths](http://habitica.fandom.com/wiki/Guidance_for_Blacksmiths) - an introduction to the technologies used and how the software is organized.
* [Setting up Habitica Locally](http://habitica.fandom.com/wiki/Setting_up_Habitica_Locally) - how to set up a local install of Habitica for development and testing on various platforms.

Habitica's code is licensed as described at https://github.com/HabitRPG/habitica/blob/develop/LICENSE

**Found a bug?** Please report it in the [Report a Bug guild](https://habitica.com/groups/guild/a29da26b-37de-4a71-b0c6-48e72a900dac) rather than creating an issue (an admin will advise you if a new issue is necessary; usually it is not).

**Have any questions about Habitica or its community?** See the links in the [habitica.com](https://habitica.com) website's Help menu or drop in to [Guilds > Tavern Chat](https://habitica.com/groups/tavern) to ask questions or chat socially!

# This fork
===============

## Summary

> This fork attempts to create next generation Habitica Pets.

## Motivation

As of this writing, Habitica pets are represented as dictionary keys inside the user schema. This approach limits the flexibility and scalability of the pet entity. To make the source code adaptable to richer ( both future and current ) feature requests, a separate model schema is needed.

Having a separate schema will have the following benefits:
 - Scalable abstraction
 - Pets can have more attributes other than "growth"
 - Pets can be easily created and tweaked.
 - Assets can easily be referenced by the Artisans / Admins through an admin UI. No need to include every asset in the source code.
 - If assets are attrib of a pet, the use of image hosting providers such cloudinary can easily be implemented. This could potentially cut back the requests received by the main server.
  - Also, this could serve as a peaceful trial run ( since pets are pretty static, have no buffs etc... ) for future attempts to create independent models for gears, items, armors, quests, etc. 

## Implementation

While bouncing around the repo, I have noticed that the code for the pets are already well established and introducing the new schema would result to lots of unwanted side effects. So the safest option as of now would be to just add a new set of pets, instead of replacing the old ones. ( This is the reason why I call it next gen pets, instead of Pets v2). Pets that were saved via the dictionary will still function as the regular pets. While pets which were saved in another collection will function as next gen pets.

(( But I guess, in the user-end perspective, having two distinct pets category would require a differentiating aspect. Maybe add a small feature to the next gen pet ( e.g. lore, ability to name it, type, class, etc) . ))

But if adding a new set of pets is not a good idea, it would still be better to make the dictionary coexist with the collection so that the old setup will still work while the contents are being migrated to the collection.

Here are all the things that I think needs to be implemented. I've been exploring around the repo for only a few days, I am very positive that I missed something, so please feel free to point it out and add it to the list.
  
**Server**
  1. Schema for Pets (obviously)
  2. Additional field inside user schema referencing owned Pet.
  3. Pet API endpoint
  4. Pet Controller
  5. Middleware to check if user has permissions to access Pet collection.
  6. Ops on Pet
     - hatching
     - feeding
     - mount

**Client**
  - Admin UI for admins and artisans
  - Page for Artisan / Admin UI
  - Modify Stable for Pets.
     - Next gen pets have no limit so better pagination and search is needed.


I know that this is a lot of work and this stuff is not that important. But I think having separated model from the user will be a good first step and a promising investment to address the ever increasing creative inputs from the Habitica community. I have started implementing this on my own but since I am most familiar with the MEAN stack, coding with vue will take some time, so if you are eager to help me please contact me or submit a PR. Thanks :)