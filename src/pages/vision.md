This is my attempt to explain what Specky is, or should be, and how we can get there.

## The Problem

I've been 'vibe coding' for a while now, and one of the things I've noticed is that I'm no longer a developer, I'm an author! 
I'm endlessly writing specifications (some call them Product Requirement Documents - PRDs) or instructions that the agent needs 
so it can go off and do its job. There are now a number of tools to help generate PRDs, so alongside my new job as an author, 
I've also got a job as an editor! I'm constantly reviewing generated specs and, if you want to do it properly, it's a lot of work! 
I would love it if I could just get the requirements for "Thing X" and be able to trust that someone has spent some time 
thinking about it and created a solid, tested specification.

I've also noticed that the various LLMs tend to produce poor results when you leave the "beaten track" and start dealing 
with requirements that aren't very well documented. A friend shared a good example of this. He's an avid paraglider and is 
building an app that he takes with him on his flights. He's using a weather service API to get some obscure weather data, 
and all the LLMs he tried had no idea about it and couldn't produce any sensible code. He tried really hard but ended up 
having to go and document the obscure format himself so he could give it to the LLM.

Wouldn't it be great if there was a repository containing the requirements for **everything**, so we could just fetch them 
and give them to our coding agents without having to worry about missing something?

## The Solution?

For the sake of clarity: the idea with Specky is to package **requirements** so we can combine them and give them to our agent 
coders to build our applications. Well-defined requirements should (hopefully) lead to more robust, complete applications. 

## Here's what a solution might look like

Let's say I'm building a website for my over-enthusiastic boss. We're building some fancy SaaS solution, but "it definitely needs a blog!" he says. "And also an online store. Plus a whiteboarding tool like Miro or Mural. Our customers would love that!"

I go to the Specky repository and download/install the following components:
- blog
- store
- whiteboard

I inspect the store component and see that it depends on a number of other components:
- catalog
- shopping-cart
- checkout

That's very interesting, I think to myself, then I run the Specky CLI, and it goes off and builds a nice detailed specification document for me with all the various requirements and use cases and even some tests. I then tell my coding agent to go and implement the whole thing in Rust because my boss thinks Rust is awesome, and off we go!

## Potential Goodness

Apart from saving you time trying to figure out and carefully declare how everything should work, I can see a few interesting side effects.

1. **Your programming language is now irrelevant:** I could, for the sake of argument, just implement everything in Rust from now on. I don't have to worry if there's a weather service library for the software stack I'm using. I just roll my own.
2. **Set knowledge free:** we would essentially be packaging business knowledge here. Anyone can learn about Swiss tax laws by reading the relevant spec.
3. **Is this the next layer of abstraction?** We started with punch cards, then came assembly, then low-level languages like C, then higher-level languages like Java & C#, and finally Python. I'm aware they to some degree in parallel, but with each step along the way developers spent less time dealing with talking to the machine and more time just declaring what the machine should do. Is the final step just declaring requirements in (structured) natural language?

## Potential Badness

### What goes in the Repository?

I can already see a few problems with Specky. Here's what I'm thinking...

There are different classes of applications:
- CLIs
- Servers/APIs
- Web Frontends
- Mobile Apps
- etc.

How do we (or do we even want to) decouple the requirements from the type of application (essentially the architecture) we're building? In the case of a web application, I might have some sort of a multi-step user flow that I want to specify. That just doesn't make sense for an API. Does it make sense to try to boil these down to pure, requirements without any reference to technical architecture? Do those sorts of things not belong in the repository? My instinct is to just let the thing evolve, but I would prefer to catch any potential errors early. 

### Security

Do we need to worry about security? Specky would be a good target for prompt injection attacks, but maybe that's something we can deal with downstream? There are enough security scanning tools out there that work on code bases - maybe that's enough? On the other hand, scanning packages for dangerous prompts might not be so difficult, but we'll always be rushing to detect the next prompt attack. I'm not trying to develop an a prompt scanner - someone else should go and make millions doing that (don't forget me when you're rich!).

## How should it work?

If you check out the [documentation](docs/intro) you should get a better idea of how Specky **should** (might?) work.

## Collaboration

I've taken a lot of inspiration for Specky from NPM (Node Package Manager). They have an [RFC process](https://github.com/npm/rfcs) that allows anyone to contribute in an organised, somewhat democratic, way. I want to do the same for Specky.

I'm open to alternatives though. I just want to set this thing free in the world and let it evolve with the state of the art.

## Contact

If you want to contact me to provide feedback or share ideas, best would be to connect with me [via LinkedIn](https://www.linkedin.com/in/james-barnes-ai). 

Looking forward to hearing from you!