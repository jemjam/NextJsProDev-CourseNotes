## [Next.js Foundations for Professional Web Development](https://www.pronextjs.dev/workshops/next-js-foundations-for-professional-web-development~lxb18)

The first module for the [[ProNextJs.dev Course Review]] covering high level basics about Next.js app and rsc architecture

- Small typo on page one. (I think? submitted via course feedback widget)
  > all of the most important parts of working **WITH** Next.js.

[Welcome to Pro Next.js](https://www.pronextjs.dev/workshops/next-js-foundations-for-professional-web-development~lxb18/welcome-to-pro-nextjs)
- First video: setting the quality, looks really good.
- No exercises here, just setting the stage for what's to come
- strongly recommends doing the exercises along with to gain practical experience

[Why You Should Choose Next.js](https://www.pronextjs.dev/workshops/next-js-foundations-for-professional-web-development~lxb18/why-you-should-choose-nextjs)
- Talks about some of the pros of nextjs over other "server rendered" frameworks
- Highlights include react server components, hybrid rendering modes, parallel routing, partial prerendering and streaming
- (compared against waku/remix/redwood) -- frames Next.js as the best solution for server rendering react applications

[When Not to Use Next.js](https://www.pronextjs.dev/workshops/next-js-foundations-for-professional-web-development~lxb18/when-not-to-use-nextjs)
- some obvious cons though
- requires hydration: excess data is returned as additional data
- highly interactive: this is server rendered framework first (with rsc especially)
- lots of features/overhead for a fullstack framework, if you're not using them then lighter solutions may be appropriate

[The React, Next.js, and Vercel Controversy](https://www.pronextjs.dev/workshops/next-js-foundations-for-professional-web-development~lxb18/the-react-nextjs-and-vercel-controversy)
- vercel has a very close relationship with react core team members
- got to use RSC early because of that close relationship
- as other frameworks start to adopt RSC, hopefully the concern dies down a bit
- > This course is not funded by Vercel, and the instructor has no financial relationship with the company.
	- 🌟🌟 This is actually really big for my trust in the course, as the module lays out some of those concerning "conflicts of interest" and makes it clear that they are not affiliated 🌟🌟

[Create and Deploy a Next.js Application](https://www.pronextjs.dev/workshops/next-js-foundations-for-professional-web-development~lxb18/create-and-deploy-a-nextjs-application)
- getting into some practical code finally, setting up a repo locally with create-next-app
- recommends installing `@latest`: hopefully these modules are kept up to date 🤞🏻
- 😕 🔖 -- starts with `pnpm dlx` but then in the second command (add shadcn), uses npx?
- Sent a note using the feedback widget:
	- ```text
	  run the following command:

	  npx @shadcn/ui@latest init

	  Jack has it right in the video, but it’s wrong in the text. Should be: shadcn-ui@latest. The scoped package leads to an error: “unknown command ‘init’”.

	  It also seemed strange to use pnpm dlx for the first command but then shift to npx for this one. (both can use pnpx?) I’m probably nitpicking tho.
	  ```
- doing some digging after the fact, it seems it's not uncommon to just `npx` even as a pnpm user.

[An Overview of the First Application](https://www.pronextjs.dev/workshops/next-js-foundations-for-professional-web-development~lxb18/an-overview-of-the-first-application)
- Showcases the app (no instruction)

[Create Your First Route](https://www.pronextjs.dev/workshops/next-js-foundations-for-professional-web-development~lxb18/create-your-first-route-ioxzw)
- Jack shares an example but then gets you to build the **about** route yourself
- It's as simple as adding a new folder with a `page.tsx` within for the page content

[Add a Header Using Layout](https://www.pronextjs.dev/workshops/next-js-foundations-for-professional-web-development~lxb18/add-a-header-using-layout-gekfe)
- Starts with Jack sharing how he adds the about page (just to reinforce) 👍🏻
- Then showcases the root `layout.tsx` and adds a header with some minor styling around stuff
- Pushes the code to github, which then triggers the vercel build
	- (really showcases how optimized vercel is, makes this stuff too easy)
- teases that we're going to add some auth in the next video (nextauth)

[Choosing a SSR Framework or a SPA System](https://www.pronextjs.dev/workshops/next-js-foundations-for-professional-web-development~lxb18/choosing-a-ssr-framework-or-a-spa-system-4yeja)
- compares nextjs to rendering a react app with vite
- shows the vite build fails with js disabled
- the next build prerenders and sends static markup, then rehydrates that markup
- Includes a `use client` components
	- EMPHASIZES that client components run twice, both on the server and the client.
	- (The server renders it to static markup, that's the first render.)

[Client vs. Server Components in Next.js](https://www.pronextjs.dev/workshops/next-js-foundations-for-professional-web-development~lxb18/client-vs-server-components-in-nextjs)
- sets up a new create react app and then shows off the differences between a server and a client component
- Only client components run on the client. (they also run on the server)
- Puts a console log in a ClientComponent vs a ServerComponent:
	- you can see the two logs (for both) on the server (likely during prerender)
	- There is no log initially on the client until the `use client` directive is added
- ⚠️ You can only use hooks on the client
- Server components can pass props to client components: everything works EXCEPT passing functions

---

[Add Authentication with NextAuth.js](https://www.pronextjs.dev/workshops/next-js-foundations-for-professional-web-development~lxb18/add-authentication-with-nextauthjs)
- Continuing to build up the chat application, adding auth
- Add the package and generate the initial local secrets
- Using github as the login method, separate tokens for production / local
	- makes the local env file for local dev
	- as well as setting env vars in vercel
- create the nextauth route handler, etc

[NextAuth v5 Update](https://www.pronextjs.dev/workshops/next-js-foundations-for-professional-web-development~lxb18/next-auth-v5-update~tiw2k)
- Minor update for some of the new next auth apis
- 😕 as an outsider, next auth vs auth.js is mildly confusing, but probably outside of scope to discuss in this course?
- just goes through how to work with the adjusted apis

Exercises: adding auth
- mostly just followed the docs after the v5 update video
- a little misstep as I tried to follow next-auth 5.0 directions, but only installed 4.x with @latest. (5 is still in beta)
- got it all working w/o too much difficulty

---

[Composition in Next.js: Understanding Client and Server Components](https://www.pronextjs.dev/workshops/next-js-foundations-for-professional-web-development~lxb18/composition-in-nextjs-understanding-client-and-server-components)
- Okay, so this one is about the different between the client and server component models.
- Client Components Can't Invoke Async Server Components Directly:
	- ie you can't put the server component in a client component render method
- When a client component invokes another component, that component automatically becomes a client component.
  background-color:: yellow
- However, you can pass the server component as children / props, which will render fine

[Intro to Server Actions](https://www.pronextjs.dev/workshops/next-js-foundations-for-professional-web-development~lxb18/intro-to-server-actions)
- creating another side-demo again to show off some of the nuances of server actions
- a small todo list with add todo (that writes the json file to disk)
- server actions: functions cannot be passed directly to client components
- can tag the function with "use server" so that it's invoked on the server
- -- once adding elements to the json is working, it doesn't show immediately --
	- need to revalidate the path
- `revalidatePath` from `next/cache`: one option, based on path alone
- `unstable_cache` and `revalidateTag`: tag/resource based
	- similar to react-query cache style, you wrap your function in a caching function and can tag the results.

[Add Interactivity with Next.js Server Actions](https://www.pronextjs.dev/workshops/next-js-foundations-for-professional-web-development~lxb18/add-interactivity-with-next-js-server-actions~gbhrx)
- server actions in a little more depth
- adding a whole folder for server functions
- "use server" can either be top of file, or just inside the top of individual functions
- showing the build for a really basic chat interface that uses the server actions to communicate
- DONE Run through this exercise where we
	- install openai, configure a chat completion,
	- and update the local chat component with the results as they come in.
	- (no persistence yet)

---

[Store Chat Data in a Database](https://www.pronextjs.dev/workshops/next-js-foundations-for-professional-web-development~lxb18/store-chat-data-in-a-database)
- addressing that there's no persistence yet
- DONE Exercises
	- creating a vercel postgres store
	- vercel cli installed, and adding the packages to the env

---

[File-Based Routing with App Router](https://www.pronextjs.dev/workshops/next-js-foundations-for-professional-web-development~lxb18/file-based-routing-with-app-router~dtnrx)
- talking about the router patterns inherent to next js
- page.tsx or route.tsx at whatever path
- going back through a separate demo app to demonstrate some of the routing concepts
- 🏁 lots of callouts to ensure you're actually working on the projects alongside
- video is all about the different file based routing conventions: mostly put your page/route into folders and that's your urls.
- (plus parameter `rout/[param]/page.txx` / catchall `rout/[...params]/page.tsx` routes)
- optional catchall routes use double brackets: `[[...optional]]`

[Adding Parameterized Routes to a Next.js App](https://www.pronextjs.dev/workshops/next-js-foundations-for-professional-web-development~lxb18/adding-parameterized-routes-to-a-nextjs-app)
- Adding the routes for individual chat pages (by id)
- ```tsx
  export default async function ChatDetail({
    params: { chatId },
  }: {
    params: { chatId: string };
  }) {
    const chat = await getChat(+chatId);

    return (
      <main className="pt-5">
        <Chat id={+chatId} key={chatId} />
      </main>
    );
  }
  ```
- (the `+` before chatId is coercing it to a number)
- talks about how to make routes `dynamic` to force them to always requery the data
- `useRouter` to redirect. `notFound()` to pop a 404

---

[Access Data with React Server Components](https://www.pronextjs.dev/workshops/next-js-foundations-for-professional-web-development~lxb18/access-data-with-react-server-components)
- working on a page to show the list of existing chats
- some refactoring the components of the chats
- Making a server component for PreviousChats
- An example of using <Suspense> to allow some out of order page loading

---

[Implement Parallel Routes for a Chat Menu Sidebar](https://www.pronextjs.dev/workshops/next-js-foundations-for-professional-web-development~lxb18/implement-parallel-routes-for-a-chat-menu-sidebar)
- showing a parallel route case
- the folder name starts with @, eg: `@chats`
- which makes `chats` the prop available to the `layout` and will be rendered
- loading.tsx -> Is like the fallback for suspense when the route is taking it's time

---

[Implement Streaming AI Responses](https://www.pronextjs.dev/workshops/next-js-foundations-for-professional-web-development~lxb18/implement-streaming-ai-responses)
- some changes to using the chat components with streaming that are available with the vercel ai kit
