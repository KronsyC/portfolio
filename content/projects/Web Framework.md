+++
title = "The Minty Web Framework"
subtitle = "The time it all *clicked*"
description = "The Minty Web Framework is a backend web framework that Samir Bioud developed when he was 15 during the Covid-19 lockdown, as he was really bored and wanted to learn something new, and make something exciting"
draft = false
+++



# The Minty Web Framework
My plunge into developer tooling

## Context

Back when I was 15, the thing that I spent most of my time doing, was developing backends for various little side projects that I was making. While doing so, I discovered this really cool backend library callled [Fastify](https://fastify.io). It is very similar to the traditional express.js backend, except it performed an order of magnitude faster, which intrigued me deeply, so I decided to look into how fastify could perform so much better than the most popular library right now.

I found their routing library, [find-my-way](https://github.com/delvedor/find-my-way), which used this awesome data structure called prefix trees (or trie) in order to route much more optimally than the express.js router. At this stage I had no exposure to data-structures or algorithms at all, past a basic list or dictionary, so this was absolutely mind-blowing to me. It is this moment of realization that I believe properly launched my interest in programming.


## What I Did?


#### Router
With my newly enlightened little brain, I decided that I would attempt to build my own routing library, similar to find-my-way, but my own. And I did just that, this routing library ([Beetroute](https://github.com/KronsyC/beetroute)) also utilized prefix trees internally, and supported having arguments in the request paths, although im not sure how well that extraction code would hold out. This was the very first time I have ever knowingly utilized data structures to my advantage, and it felt good.

---

#### JSON validation
After this I decided, why not take this project further? And so I decided to build an entire backend development ecosystem from scratch (In hindsight, I was much too aspirational and did not get this far, but it was my primary motivation). The next component of this that I decided had to be built was a JSON validaton library ([Schematica](https://github.com/KronsyC/schematica)). To do so, I looked to the current most popular solution, AJV, for inspiration. Upon inspecting their codebase I learned that they construct javascript functions at runtime to validate JSON objects incredibly quickly. I implemented a similar system, which from what poor benchmarking a knew how to do at this time, performed marginally better than AJV. But this was traded off by the fact that my library did not conform to the Json Schema Spec, like AJV did. But overall, this was probably my favorite component of this entire project.

---

#### HTTP Unified API
The next thing I wanted to do was actually build the web server library responsible for handling http requests. I wanted this library to support both HTTP1 and HTTP2 protocols, so I built a simple wrapper library around the node.js standard http1 and http2 modules, to make handling both requests interchangably much easier. I did also want to implement HTTP3 (Quic) support for this wrapper, but at the time, Node.js had practically no support for it, and im pretty sure it still does not support HTTP/3.

---

#### Web library
After building the HTTP wrapper library, the next logical step would be to construct the actual library, so I built the [WebMint](https://github.com/KronsyC/minty/tree/main/packages/web) library as my alternative to fastify. At this point I was also experimenting with Monorepos, which I now know I do not like working with (specifically for node.js). This library supports all the standard features you could want from a backend library:
- Request Handling 
- Static file serving
- Dividing your app into subapps
- Custom 404 handler
- Server event handlers (intercepts)
- Plugins
- Custom HTTP method support
- Response MIME type inference

I also quite heavily benchmarked this library, using the same benching tool that fastify uses, but I was disappointed to discover that my library underperformed against fastify, even after extensively optimizing the hot code paths. This has greatly increased my appreciation for the maintainers behind fastify, as I now know that they write some really damn good node code.

---

#### Web Library Decorator Wrapper
The final component of this system that I created was a library inspired by Nest.js, which wrapped my web library with a fancy decorator API, although it appears that this component never made it onto github. This is because I never felt like I got it to a good enough state to consider publishing it. But from what I remember all it really supported was the ability to define new contexts and route handlers using classes and decorators instead of the old function calling approach. It also had directory-based routing, where routes would be automatically defined depending on a files path in the file system.

## Conclusion

At this point, I began to understand the infeasibility for me to create a backend ecosystem strong enough to compete against the likes of fastify, and my interests had began to shift around. I was sick of developing for the web, and wanted to branch into other things, outside of my comfort zone, so I got into virtual machines.

Overall, I belive that this project was massively advantageous to me as a developer, and is what made it all \*click\* for me. I feel that this was a very productive way to spend a couple of months of my time during the covid lockdown. The only regret that I have is that I didn't finish it off.

If I was to go back and do it again, I would make a web framework for rust instead of javascript, as that is my language of choice now, and I would be able to squeeze much more performance out of it.

