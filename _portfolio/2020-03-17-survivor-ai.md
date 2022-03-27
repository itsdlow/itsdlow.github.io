---
collection: portfolio
title: "Survivor AI"
excerpt: "An implementation of artificially intelligent survivors in a zombie survival game<br/><img src='/images/survivor-ai-thumbnail.PNG'>"
image_title: "Walk-through"
image_url: "/images/SE475-Project3_UML.png"
---

## The Experience

This project was very challenging and fun to work on, especially as my first formal introduction into AI. This project was assigned in a 10 week course on artificial intelligence in game development and as such involved solely implementing the "brain" behind the survivor characters in a already created zombie wave survival game. In this assignment I implemented a complex decision tree as the "brain" of the survivor characters, with capabilities of offense, defense, and movement dependent on the survivors' conditions, with intentions of turning this into a goal-driven behavior system (11/20). The survivors movement was dependent on a Point of Visibility (POV) layer on top of Unity game engine's already existing NavMesh. To traverse this POV graph, I implemented a weighted A* pathfinding algorithm.  

### Strategies
- A* pathfinding algorithm
- Decision Trees

![Zombie Game - Debug View][image_url]

[image_url]: /images/survivor-ai-image.PNG