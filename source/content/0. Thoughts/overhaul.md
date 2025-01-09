---
title: Overhauling the Site
created: 08, Jan, 2025
modified:
  - 09, Jan, 2025
---

> TLDR:
> 
> I am going to try spinning my own static site generator that parses Obsidian markdown files into html files but with (ideally) no javascript present.

For the past couple of days, I've been consuming a ton of writing from [rachelbythebay](https://rachelbythebay.com/) - it's a great resource if you want to learn about reliability and other system administrator concerns. Most recently, she posted a piece called "[Web page annoyances that I don't inflict on you here](https://rachelbythebay.com/w/2025/01/04/cruft/)", which planted the seed in my head.

That and a few other pieces by her, talking about usability and complaints about web sites (I'll try to find some examples and edit this), really sparked the growth of that seed. Part of it is this: I'm currently using a fork of [Quartz 4](https://quartz.jzhao.xyz/) - which is an excellent tool - to handle this site's generation. But here lies the problem: it uses languages and tech that are outside my domain knowledge. 

Why is this a concern?

## 1. Dependence on things out of my control

![[{E3917337-82EF-4DA3-BCDE-029447895249} 1.png]]

I noticed this while watching the "Actions" tab when pushing a change to the site. Now, there probably is a commit in the works by the Quartz author to fix the backend that uses the correct version, but the transition was announced back in September, started in December and will complete on January 17th, or: in 8 days.

I don't know just how breaking this change could be: either minor or major, until it goes live.

But stopping to think about it, what is this site:

- few screen shots
- some markdown files converted to html
- some Typescript to generate some of the "would be nice" features
- some CSS files to style the whole thing

If I were "done" with this project, as in never having to trigger another build, the site would remain as long as gitpages did its thing and I don't delete the repo. On the other hand, this is a relatively simple site: updates to it shouldn't really depend on versioning changes of anything. Its not like an app where changes to the OS require overhaul of some backend code, and a great example of that is Rachel's site.

From what I can tell, its basically unchanged (other than content) from when she launched it back in 2011. If I recall correctly, she has changed some of the physical hardware over time, but the workflow and presentation itself is largely unchanged.

## 2. Little things in Aggregate

One of my personal goals (if not soon to be requirements), is that this site is easily accessible: both from the software/internet side of things and from a usability approach. I currently don't have a way to test the content with something like a screen-reader (and to be honest I have yet to dig deeper into this), but knowing that some scripting is involved, I have doubts that it'll pass.

The other side of that is: this site should be lightweight which means fast load times. It should also, in theory, mean fast build times as well. The current average build time (from push to deployment) takes ~2 minutes. That's not an egregious amount of time, but it adds up, especially when you're trying to fix an issue with the displaying of content.

The easy example here is using KaTeX to render some of the equations in the [/phyiscs/](https://quantumrook.github.io/Physics/) directory. Depending on the last time you looked at it, you may have just seen a whole bunch of red colored text and gibberish. I believe its now all fixed, but making small tweaks to the LaTeX math environments and then testing to see if that fixes the problem adds a lot of friction.

If you get it right on the first try: hey, that was only like 3 minutes tops. If you don't, and it takes 3-4 tries, it can really interrupt the flow of what you were doing. Imagine working on an assignment, saving your changes to that document/file and then having to wait 2-3 minutes before you can look at it again and see that you made a typo. That's another 2-3 minutes before you can start (after fixing the typo) again.

I don't know for sure, which ties back into point 1, but I get the sense that the build process rebuilds everything from scratch instead of just looking to see what files have changed. Some of this might come from supporting some of Obsidian's features, like linking (and displaying) content from other pages, but the source code is a bit nebulous to me on how exactly it handles this, so I can't say for sure one way or the other.

## The goal

So, to reiterate my requirements:

- simple html with simple CSS
- image support
- code block support
- local testing
- accessibility
- math support

## The plan

I do realize that what seems simple in programming, most of the time, ends up being far more complex. However, this is also a great learning experience along the way. Fortunately, I have a decent amount of experience from making websites when I was younger, so the HTML and CSS side of things *should* be straightforward - because I am aim for a simple concept.

The tricky bit comes from wanting to spin my own "markdown to html" conversion tool. Ideally, I only want to rebuild the html if the source markdown file changes, but supporting the cross-page content linking is going to add some complexity to that.

I have faith that I can get it working, the trick is going to be able to ultimately have the process take less time than the current implementation.

The other tricky bit is going to figuring out how to render math equations. I really would love to do it without having to require any scripting, but this might be an instance of: get the version working using KaTeX/MathJax, and then work on alternatives.

Since this is going to be an interesting project, I will attempt to document and do a mini-write up as things progress, and then hopefully polish the result once the transition is complete.

And with that, it's time to get started - only 8 days left!