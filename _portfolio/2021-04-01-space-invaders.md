---
collection: portfolio
title: "Space Invaders"
excerpt: "A modern, object-oriented implementation of the 1978 Space Invaders game<br/><img src='/images/space-invaders-thumbnail.jpg'>"
video_title: "Walk-through"
video_url: "https://www.youtube.com/embed/d8jyep9MhIc"
file_url: "files/SE456-Design_Document.pdf"
file_type: "application/pdf"
last_update_date: "April. 2021"
---

A robust recreation of the game Space Invaders developed with a barebones game engine, TEAL, based on the SFML framework. This application implements numerous design patterns to enable testing, maintainability, and expansion of the game with ease.

{% if page.video_title and page.video_url %}
	{% include {{ page.video_include }} url=page.video_url title=page.video_title %}
{% endif %}


## The Experience

This project was the result of 20+ hours per week of work in a 10 week architecture of real-time sytstems course at DePaul University.


### Object-Oriented
- The goal of this project (besides recreating the arcade game) was to use as many design patterns as possible. In total, over 10 different design patterns were used, including: Singleton, Flyweight, Iteratoor, Strategy, Null Object, Factory, Proxy, State, Visitor, Adaptor, Observer, Command, Composite, Object Pools, and Template.

### Optimized Collision System
- There are numerous different systems throughout the project, all of which are described in the pdf below. One of these is the collision system, which makes use of the composite pattern to create group axis-aligned bounding boxes (AABBs) that are checked before iterating any child objects. This reduces the number of collision checks required per frame, with an "early-out" strategy.

{% assign rel_url=page.file_url | absolute_url %}
{% include {{ page.file_include }} url=rel_url media_type=page.file_type update_date=page.last_update_date %}
