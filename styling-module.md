# Styling Next.js Applications with CSS

Module two from `ProNextJs`, continue of [ProNextJs Course](./README.md), exploring styling solutions

## Note Summary
Covers styling solutions at multiple touch points of the stack

## Individual Modules

[Styling Next.js App Router Applications](https://www.pronextjs.dev/workshops/styling-next-js-applications-with-css-dylwm/styling-nextjs-app-router-applications)
- introducing the module
- goal is to take a stack of product, but build out a responsive layout
- media and container queries, and light and dark mode

[Create a Layout with CSS Modules](https://www.pronextjs.dev/workshops/styling-next-js-applications-with-css-dylwm/create-a-layout-with-css-modules)

- there is a starter that has some code to build from
- first video showcases css modules, a short explanation of how they're used
- short exercise for the viewer to apply some of the card classes to the component

[Refine the Layout with CSS Modules](https://www.pronextjs.dev/workshops/styling-next-js-applications-with-css-dylwm/refine-the-layout-with-css-modules)

- Continuing to refine the designs
- adding a little to a reset
- using container queries to style the cards
- `container-type: inline-container` and then going by whether it's horz or col
- ❗ using way too many divs in this template, it would be nice if it was slightly more semantically oriented
			background-color:: yellow
- I thought he was using layouts based on aspect ratio, but they're actually just a small width and large width versions
		- even though they're simple queries, they're still tied to the _container_
- prefers-color-scheme: dark: very basic implementation swapping black and white
- "predictable and reliable approach to styling"

[Getting Started with Tailwind CSS](https://www.pronextjs.dev/workshops/styling-next-js-applications-with-css-dylwm/getting-started-with-tailwind-css)
- same example, but using tailwind this time
- installing tailwind: some instructions and explanation about the differences with tailwind 4
- configuring tailwind locally
- get our css reset applied immediately
- shows an example of dark and light mode with the tw dark and light prefixes (super easy!)

[Configure Container Queries with Tailwind CSS](https://www.pronextjs.dev/workshops/styling-next-js-applications-with-css-dylwm/configure-container-queries-with-tailwind-css)
		id:: 66cd4459-7413-4339-954e-7a12cdf7d6f7
- @container queries example
- doesn't really work initially because tailwind v3 doesn't include container queries by default (you can include a plugin)
- (goes and installs the plugin for v3, proclaims that v4 thankfully includes it)
- apparently inside tailwind they use css modules? no way!

[Combine CSS Modules with Tailwind CSS](https://www.pronextjs.dev/workshops/styling-next-js-applications-with-css-dylwm/combine-css-modules-with-tailwind-css)
- showing tailwind with @apply styles in css modules
- css module names in the template, but the important styles applied via @apply
- I disagree with jack over whether this makes the templates more readable
		- it might look nicer, but it's an extra step to map what those classes are actually doing
- this is an indirection that I think nobody should be shown, seems like an anti-pattern

---

### CSS-in-JS - Build Time

[Intro to Meta's StyleX](https://www.pronextjs.dev/workshops/styling-next-js-applications-with-css-dylwm/intro-to-metas-stylex)
- good for very large company, or oss
- locked in and defined styles -- feels a lot more strict than css and tailwind
- setup
- `npm install @stylex/nextjs-plugin@beta`?
- changes from the code he's showing: ==just follow instructions from stylex site==
- stylex is a babel plugin - it takes us away from swc and back to webpack (little slower)
- establish reset in globals
- showing creating the dark/light mode styles with stylex
- `stylex.props` to pass styles
- Fonts not supported so he just dropped it for now (that seems like a potential blocker)
- 💬 honestly, to me it seems like this one isn't really worth the effort

[Finish Styling with StyleX](https://www.pronextjs.dev/workshops/styling-next-js-applications-with-css-dylwm/finish-styling-with-stylex)
- can't use shorthand syntax for anything with styles, wants very granular control 👮🏼
- stylex is designed for precise design systems that is very controlled, for meta's size
- harder to use generally, but good if you really want those constraints
- 🤣 "a css straight jacket"

[Styling with Material UI's Pigment CSS](https://www.pronextjs.dev/workshops/styling-next-js-applications-with-css-dylwm/styling-with-material-uis-pigment-css)
- Material UI didn't work with RSC initially
- pigment.css -- buildtime css solution from material
- `material-ui / packages / pigment-css-react` module installed, part of monorepo
- `withPigment` call put into the next.config.mjs file wrapping other next config
- can define css using the object syntax, or backtick interpolation method (more familiar)
- this one feels the most like emotion to me (tho it works properly on the server)
- ⚠️ for some reason seems to be missing the transcript
  background-color:: yellow
- (used the feedback widget to call it out)

[Finish Styling with Pigment CSS](https://www.pronextjs.dev/workshops/styling-next-js-applications-with-css-dylwm/finish-styling-with-pigment-css)
- similar to material ui v5 and emotion
- styled.div or styled('div')
- showed how to implement a custom theme, which gets passed to the class definitions through a callback
- He mentioned he liked the way the markup looked with styled components

---

### CSS in JS -- Runtime

[Styling with Emotion](https://www.pronextjs.dev/workshops/styling-next-js-applications-with-css-dylwm/styling-with-emotion)
- not necessarily a great idea with app router
- but showing how it works and some of the trade-offs
- (can't use rsc)
- installing emotion libs, and creating an "EmotionRegistry" (provider)

[Comparing Emotion with Tailwind and Pigment](https://www.pronextjs.dev/workshops/styling-next-js-applications-with-css-dylwm/comparing-emotion-with-tailwind-and-pigment)
- runs into the error where context isn't available on the server, which requires shifting the whole page to `use client`
- lots of suggestions against emotion directly since runtime css is going to have a runtime perf hit
- ⚠️ despite the page title, emotion actually wasn't brought up in any way

---

### React Component Library Showdown

[Introduction to Component Libraries](https://www.pronextjs.dev/workshops/styling-next-js-applications-with-css-dylwm/introduction-to-component-libraries~enrup)
- ⁉️: ...styling for your Next.js App *Writer* app is to...
- talking about the benefits of just using a component library vs manual styles
- introducing a small project with a form to add posts and layout around it
- 💬 ⁉️:  All right, I'll see you over in the **chat to see an** example.

[shadcn/ui - Blog App Overview](https://www.pronextjs.dev/workshops/styling-next-js-applications-with-css-dylwm/shadcn-ui-blog-app-overview~1mebq)
- mentions that it's sorta/kinda coupled to next (the primary contributor works there)
- different from other components libraries in that it copies source code into your project (for you to then customize as necessary)
- shadcn is very light wrapper that uses tailwind and radix (headless ui lib) under the hood
- goes through basic app setup, provides some files with basic typedefs
- datastore is purely in memory for this one
- making server actions for the functionality (so they're all async, not just contrived)
- using react-hook-form for the form functionality
- ==integrates really well with tailwind== (etc): good options if you use radix/tailwind or you want to

[Park UI](https://www.pronextjs.dev/workshops/styling-next-js-applications-with-css-dylwm/park-ui~i659j)
- [Park UI](https://park-ui.com/)
- also built on tailwind underneath (but panda and arc-ui also?)
- [Panda CSS - Build modern websites using build time and type-safe CSS-in-JS](https://panda-css.com/)
- Ark ui is another library (ontop of tailwind): [Ark UI](https://ark-ui.com/)
- runs through setting it up, needs updating tailwind and ts config
- had to install `tailwind-variant` along the way to make the demo work.
- looks very much like shadcn but with ==a much broader enterprise ready component set==

[Bootstrap](https://www.pronextjs.dev/workshops/styling-next-js-applications-with-css-dylwm/bootstrap~r7kmy)
- Jack is hyped on bootstrap
- Interesting to note that bootstrap does include tailwind like utility classes now
- "bootstrap is evolving with the times"
- definitely some styling changes from the earlier examples, looks a little different
- definitely sold that bootstrap is not only possible, but has pretty nice results out of the box

[Ant Design](https://www.pronextjs.dev/workshops/styling-next-js-applications-with-css-dylwm/ant-design~zbqht)
- full featured enterprise ready component lib
- Antd registry and provider need to be set up to provide the theme
- This is a **component** framework, so you import the components
- can't use typography without being a client component ⚠️
- 💬 ⁉️:  (refers to "Andy" a few times, more "App Writer" references)

[Material UI](https://www.pronextjs.dev/workshops/styling-next-js-applications-with-css-dylwm/material-ui~hc696)
- mostly open source
- but there are paid premium add-ons that can be worth it, such as adding data-grid
- more verbose components
- current version (v5) is emotion based unfortunately
- v6 is coming with pigmentCSS system at build time
- [mui/pigment-css: Pigment CSS is a zero-runtime CSS-in-JS library that extracts the colocated styles to their own CSS files at build time.](https://github.com/mui/pigment-css?tab=readme-ov-file) which is built on top of:
- [Index – WyW-in-JS](https://wyw-in-js.dev/) -- ==A Toolkit for Zero-Runtime CSS-in-JS Libraries== which spun out of linaria [linaria: Zero-runtime CSS in JS library](https://github.com/callstack/linaria)
- (continues to setup a mui application)
- specific AppRouterCacheProvider and ThemeProvider
Default inputs use the inline placeholder pattern (and were broken in the demo)

[Chakra UI](https://www.pronextjs.dev/workshops/styling-next-js-applications-with-css-dylwm/chakra-ui~9f3ys)
- another emotion based system
- allows some overrides with util-style styling props (mb = margin-bottom):
- except he talked about adding padding with margin
- despite being emotion based: has good app router support and works for server components
- ⚠️ flash of unstyled content with emotion underneath

[Wedges](https://www.pronextjs.dev/workshops/styling-next-js-applications-with-css-dylwm/wedges~3h3o2)
- from lemonsqueezy!
- built on tailwind
- huge set of components and compat with many frameworks
- going through the install steps yet again
- unlike shadcn you actually do still use their components

[NextUI](https://www.pronextjs.dev/workshops/styling-next-js-applications-with-css-dylwm/next-ui~h0iz1)
- lots of beautiful components, very rounded input elements
- base install brings in a lot of boilerplate
- ⚠️ required a "suppressHydrationWarning" addition to make it work
- component library: individual components for each element of the form
- ⚠️ also has premium components that can be purchased

[Mantine](https://www.pronextjs.dev/workshops/styling-next-js-applications-with-css-dylwm/mantine~uppnj)
- broken into lots of sub components
- commercial grade and ready to go
- postcss is used for styling
- 😖 mentions that installing tailwind would include postcss for free, but then would have to be removed (chicken before egg)
- true "component" library: you add components for elements, you add components for layouts, etc
- mantine `useForm` is just like react-hook-form
- nice and easy to set up, easy to use
