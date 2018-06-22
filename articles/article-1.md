# Article 1/5: My first hackathon!

This is the first article of a short blog series where I will be sharing my experience, interesting findings and much more about frontend development. This series is part of an assignment for my “Everything Web” Minor course. I really hope you guys enjoy reading it as much as I enjoyed writing it.

Today I will be talking about my first hackathon experience. This event took place on 18 May 2018 from 11 am until 4 pm. Overall it was a really successful event in my option, however, the day did not start as planned. I had a lot of transportation problems that morning. For starters, my train was canceled, with also meant that I missed both my bus and metro connections. Because of this I arrived about 20 minutes later on my appointment, missed the event introduction and most of the project's details. In the end, I choose a random project without knowing anything about it or it’s attendees, hoping for the best case scenario.

## Our assignment

After choosing a project I and a classmate joined the project owners for a short meeting. During this meeting, they explained their project, expectations and general information to us. Being the smallest group, me and my college decided to work together.

Our client's project was a simple multiplayer game where players got a randomly selected persona (character) based on multiple real-life stereotypes. It was a bit racist, for example, a Chinese that loved traveling and took pictures of everything on its way. Or the fact that building a Muslim religious building generated a security penalty. It didn't really bother me, just something I noticed. Each persona had a short biographical description with its interests, likes, and dislikes.

Players were expected to roleplay the given persona. The game itself took place after an apocalyptic event where our known world was destroyed. Working together, players can move between multiple game stages (levels) while rebuilding and shaping there own world based on their persona’s interests. It was a simple game where no one could actually lose. Each round the players should be presented with two different tasks, based on their persona they had to vote for one or the other. If the player's combined resources met the requirements for the chosen task, a building was built. Granting multiple benefits and penalties based on the task. Slowly they could rebuild the world while giving it a more personal flair.

## My job as a frontend developer

Our clients had zero programming experience and required our help to build a solid code structure and starting point for there game mechanics. Especially the tasks system and the required game mechanic calculations. The concept and design were almost completed by the time we got involved.

Given our past experience with [socket.io](http://socket.io), we decided to apply this technology to this project. Especially because there where multiple clients involved that had to communicate with each other and our servers simultaneously. In the end, this turned out to be a good choice but a bit too complicated for the product owners who had zero experience. My original goal was completing every core mechanics in the given time, especially because they were simple and easy to comprehend. However, just like everything else in life, it did not go as planned. I and my partner were really dependent on each other's work and this lead to a lot of merge conflicts, especially at the start. We had two very different coding styles and editor settings with lead to a lot of merge conflicts. Thankfully we could come up with a solid coding convention on the spot that really helped us out completing our work.

### What did we deliver in the end?

- A working [socket.io](http://socket.io) environment where multiple clients could join the game and communicate with each other.
- An personas distribution system that gave each new client it’s own unique persona.
- A basic version of the task voting system and all it’s related mechanics and point calculations.
- An overall city score system that could be used for displaying the different buildings.
- No CSS, pure HTLM and 100% ugly! (but functional)

In the end, we were a bit disappointed that we could not finish every game mechanic on time. Our clients, however, where super excited and happy with the delivered work. We even took some pictures together and exchanged our contact information for further development advice.

## Rounding Up!

After completing our assignment and meeting our deadline, we had to give a short presentation to everyone that participated in the hackathon. Even though I was quite happy with what we had accomplished there was a small problem. We had to present our work in front of unknown faces and in English! Now don’t get me wrong here, I don’t mind giving presentations, I really don’t. However, I never gave a presentation in English before. I was really nervous, but so was my partner. Knowing there was no escape, I took the lead and did my best. The assignment was completed, my first English presentation and hackathon where a success and the clients where happy. What else do you need?

## Reflection

I started working on the project without really knowing anything. We had just made a repository and each of us started doing its own thing. Soon enough we started relying on each other more and more. Because of our lack of communication, we ended up with a lot of code conflicts. I really wish we had communicated more, especially before starting to code. Doing so could have prevented a lot of lost time and without a doubt a better, more completed end product.
