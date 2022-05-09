---
collection: portfolio
title: "Memory Allocator"
excerpt: "A custom memory allocator implementation<br/><img src='/images/memory-allocator-thumbnail.png'>"
---

This project can be viewed as a memory allocator or threaded memory management library. It is an original design, intended to minimize allocation overhead, specifically for multithreaded applications. The design for this library integrates concepts from two published papers: [Hoard](https://dl.acm.org/doi/10.1145/378995.379232) by Berger et. al and [Threaded Dynamic Memory Management](https://www.researchgate.net/publication/221328632_Threaded_Dynamic_Memory_Management_in_Many-Core_Processors) by Herrmann and Wilsey.



#### Core design considerations

- Cross platform (Windows, Linux)
- ability for inter-thread malloc()/free()
- Fixed-heap design approach
- Memory management thread



---





