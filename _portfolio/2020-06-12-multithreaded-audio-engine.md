---
collection: portfolio
title: "Multithreaded Audio Engine"
excerpt: "An audio engine layer abstraction on top of Windows XAudio2 audio API<br/><img src='/images/audio_engine.jpg'>"
title: "Multi-Threaded Audio Engine"
video_title: "Walk-through"
video_url: "https://www.youtube.com/embed/lb4Lz04Od1M"
post_resource: "post_resources/Audio_Engine_Documentation.markdown"
---
An audio engine layer abstraction on top of Windows XAudio2 audio API.

XAudio2 is a low-level audio API. This application creates a more usable, multi-threaded API to interact with XAudio2, implementing the Actor model approach.

{% if page.video_title and page.video_url %}
	{% include {{ page.video_include }} url=page.video_url title=page.video_title %}
{% endif %}


## The Experience

This project was the result of 20+ hours of work in a 10 week multithreaded architecture course at DePaul University. And to date (11/20), is the project I am most proud of. As it was for a class, we were restricted to only the most basic threading tools, mutexes. And with that, were to focus on creating a clean architecture, considerate of the fact we were programming an interface for programmers to use as a extension of a game engine.

## The Architecture

### Communication between threads
- I implemented the [Actor model](https://en.wikipedia.org/wiki/Actor_model), through the use of [circular queues](https://en.wikipedia.org/wiki/Circular_buffer), _CircularData_, passing commands between my _AudioEngineThread_, the _Game_ engine thread, and the _FileThread_.


### Handle System
- A handle system was also needed for this project, using [handles](https://en.wikipedia.org/wiki/Handle_(computing)) to protect _Sound_ objects owned by the user and the _WaveSound_ objects owned by the audio engine. This projects these objects from being accessed when in a invalid state (i.e. resources have been released).

### User Interface
- A design choice I am proud of in this project, is that the user has restricted access to the real _Sound_ resource, forced to interact with it through a _GameSound_ object returned by the _SoundManager_. In addition, all interactions with the audio engine are done through the _SoundManager_ or the _GameSound_.


{% include_relative {{ page.post_resource }} %}