# ProNextJs.dev Course Review (written out)

I've had the privilege of reviewing the "Professional Next.js" course by Jack Herrington. This repository contains my notes from working through all four base modules. But in case you don't want to parse through all that, here's a brief summary.

Overall, "ProNextJs.dev" is exactly what it sounds like: a professional grade web-course that teaches Next.js from the ground up. The site works well, the videos are high quality, the sound is pretty good. I especially like the ultrawide layout showing the transcript and lesson description side by side; it's clear that the team behind this course has experience shipping high quality course websites.

This isn't the first time I've used Next, so I wasn't going in completely blind. Next is one of those projects where over time I've read the manual front to back. While I knew a lot of the fundamentals (covered in the first module), it was still good to run through building a little demo, getting our feet wet with the basic template and route constructs. I can definitely see the value here for someone coming in green.

The styling module goes into depth about how to work with styles in a Next.js app. I was initially surprised this was a whole dedicated section, but then there were a lot of example variations that did seem worth sharing. (We had everything from pure component libs, to css modules, to tailwind.) My only issue in this section was the lack of semantic markup, just doing everything with divs for the most part.

The architecture module is one to bookmark. Jack covers all sorts of tooling _around_ the Next.js project, with examples for linting, formatting, tests, etc. In particular, tests and storybook at both the component / e2e level are explored. Next.js is a beast, so I loved going through each example integration. I could sense some of Jack's former (module federation) training slipping through in the monorepo examples.

Finally: the RSC architecture block was probably the most useful to me. When I hear developers complain about unintuitive behavior, it's usually related to Next caching in some way. But Jack tackles it from all angles, providing some of those insights into how to handle more complex architectures. He frames caching as "good actually" for performance, then provides the tools to work with it at each separate layer.

The course material is all fantastic. The quality of the training platform is top notch.

Including transcripts (and video captions) makes it easier for me to engage and maintain focus. My only small complaint here was the prevalence of incorrect or misheard captions; almost anytime Jack refers to the "App Router" we instead get captions saying "App Writer". With context this is usually not a big deal, but it became cognitive load when talking about "route" vs "routeR" caches. Hopefully this is something that can be proof-read and fixed eventually.

Jack also mentions in the second to last video that he has some friends at a company that use a certain caching strategy. I appreciate the technology callout, but I'm not sure the company name is adding any value here. It's unfortunately a little alarming to hear that association, and is something that could alienate certain users. Until this point I was enjoying the course completely, but with it's inclusion I'm not sure I can recommend everyone check this out.

Overall it's a lot of great material. Next.js is covered top to bottom, including it's latest architectural patterns. Not only does this course get you up to speed with the platform, but it also touches on how this platform might fit into a variety of external architectures. This is a great resource for anybody who wants to master delivering modern Next.js
