---
collection: portfolio
title: "Tetris - Globally Distributed Software Development"
excerpt: "Distributed Software Development Project<br/><img src='/images/tetris-logo.jpg'>"
image_title: "Walk-through"
image_url: "/images/SE475-Project3_UML.png"
---
An implementation of a Tetris game based on [freetetris.org](https://www.freetetris.org/game.php)

## The Experience

This project was very interesting and challenging for unexpected reasons. This project was assigned in a globally distributed software development (GDSD) course and as such involved completing a group project in a virtual team environment. The assignment was meant to be a paritioning project, in which our division, composed of 4 seperate teams, were to divide the tasks appropriately to ensure the projects completion by the deadline. This project took place over 3 weeks, a design phase, implementation phase, and a completion/integration phase.

<br>

### My Responsibilities
- Me and the division leader of the project were responsible for designing the architecture of the Tetris game, primarily summarizing it through the use of a UML diagram which we composed together. In addition to designing and paritioning components of the architecture, I was also actively involved in the leadership of the division, reviewing work, clearing any misunderstandings with the design, and ensuring that teams were staying on pace.

<!-- Needs iframe size 770x700 TODO: supply to include -->

{% include image-large.html url="/images/SE475-Project3_UML.png" title="Tetris Game UML" %}


### Communication and Review
- The largest parts of this project was coordinating between teams, maintaining communication, and documenting information into a shared space. With that, we used Microsoft Teams to communicate and Github for version control, project issues, Actions, project board, and coordination between teams. I realized how essential and difficult it is to communicate between teams, and found several strategies essential in making it managable. One of which was requiring 1 or 2 reviews through Github Actions before merging, which was primarily done by myself and the division leader. In addition, I found the partitioning mentality to be useful, as it forced a design which was component-based with minimal coupling and few dependencies, as well as emphasizing intra-team communication and reducing some need for inter-team communication. Another useful practice we took as a division was the use of Github Issues, this help to reduce the chance of bugs and features being reported and resolved by more than 1 team.

![Issues tracking][image_url]


### The BlockGrid
- The smallest part of this project, for me, was thecoding portion, despite this, the _BlockGrid_ is an integral part of the Tetris game system, as it stores the current state of the grid and is responsible for determining any events in the game such as placed shapes, completed lines, and game over. The implementation of the grid is fairly simple, as a 2D array of _Blocks_.

### Lessons

- I think I learned quite a bit from this project, but the most concrete lessons I learned was that, as a leader of a distributed team you must actively reach out, or atleast make very clear, channels of communication. Another lesson that was learned in this project through trial and error, was that knowledge must be shared early and often. Without this, it is all too easy for teams to not understand the overall architecture of the project, especially in a component-based system. And it is essential for all members to have a high-level grasp in smaller teams, to ensure that everyone can participate during the integration phase, when work needs to be done between components (i.e. bug tracking and integration).


[image_url]: /images/gsd-issues-tracking.PNG