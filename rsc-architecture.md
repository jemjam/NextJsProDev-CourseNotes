Module Four of Four, of [[ProNextJs.dev Course Review]]

Intro: [Next.js React Server Component (RSC) Architecture](https://www.pronextjs.dev/workshops/next-js-react-server-component-rsc-architecture-jbvxk)
- going into caching strats, file uploads, architecture

{{renderer :tocgen2}}

## Caching in Depth
Caching apis:
- unstable_noStore()
- headers()
- cookies()
- export const dynamic = "force-dynamic"
- export const revalidate = 2 // Time between being revalidated
- revalidatePath and revalidateTag

[Next.js API Route Caching](https://www.pronextjs.dev/workshops/next-js-react-server-component-rsc-architecture-jbvxk/next-js-api-route-caching-adpb7)
- feels like this vid was meant to be the third one in
	- module ends with: "that covers the full route cache and how it applies to pages and routes"
- next automatically caches api routes that don't perform actions that would prevent caching
- if you want them dynamic, you [have some options](((66d0a8fc-395d-4185-a423-44694d1d26d4)))
- POST/PUT/DEL are automatically dynamic (because they act on data)

[Caching with the Next.js App Router](https://www.pronextjs.dev/workshops/next-js-react-server-component-rsc-architecture-jbvxk/caching-with-the-next-js-app-router-dtpj1)
- This seems like it should have been the first video in this sectiontal
- talks about the first one we're going to look at is the full route cache

[The Full Route Cache](https://www.pronextjs.dev/workshops/next-js-react-server-component-rsc-architecture-jbvxk/the-full-route-cache-lc3dt)
id:: 66cfc882-85cd-4ba3-a3a5-c46e3e9e06c3
- routes are either static or dynamic
- the ==build output== will show which routes are dynamic `f` vs static `O`
- `unstable_noStore()` tells next the route should be dynamic
	- access properties of the request also

[Cache-busting with Tags](https://www.pronextjs.dev/workshops/next-js-react-server-component-rsc-architecture-jbvxk/cache-busting-with-tags-nj1x5)
- next.js's unstable_cache is a persistent cache between requests
- shows how to specifically cache a thing, then invalidate that cache thing
- `getData = unstable_cache(getREALData)`
- Then you can trigger a function to revalidate the cached data on the server
- have to associate the cache with a tag (the first arg is actually just the name)
- `revalidateTag`
- 💬⁉️: This sentence reads funny:
	- > Back in the `page.tsx` file, we'll being in the button and use the `revalidateTag` function to revalidate the cache:
	- the last code block uses getDBTimeReal() but imports only `getDBTime`

[Dynamic Routes in Next.js](https://www.pronextjs.dev/workshops/next-js-react-server-component-rsc-architecture-jbvxk/dynamic-routes-in-next-js-pf2le)
- do dynamic things to keep a route dynamic
- like reading headers / cookies, or useSearchParams on the client
- export const dynamic = "force-dynamic" | "static"

[Data Caching and Revalidation with React Server Components](https://www.pronextjs.dev/workshops/next-js-react-server-component-rsc-architecture-jbvxk/data-caching-and-revalidation-with-react-server-components-pkgrz)
- next caches data from fetches: shows an example with a second background express server (separate api)
- "the DATA cache"
- 💬⁉️: "so in my IRC" -> "so in my RSC"
- `fetch: cache: no-store`
- next.revalidate = "2"  on the fetch call
- or you can "revalidatePath()"
- or you can revalidate by tag again

[The Next.js Router Cache](https://www.pronextjs.dev/workshops/next-js-react-server-component-rsc-architecture-jbvxk/the-next-js-router-cache-tkm4i)
- there is a client side cache: "the ROUTER cache"
- if you revisit a route it can be loaded from the cache super fast
- some distinction between the "route cache" and the "router cache"
	- router is client side
	- route is the server output from build that highlights dynamic vs static paths ([see "route cache" above](((66cfc882-85cd-4ba3-a3a5-c46e3e9e06c3))))
- 💬⁉️:  "It's never been an issue with the router cache, it's only an issue with the router cache."
- when a server action is executed, the client posts to the server with a specific header, then server runs with that action and responds
- ==router.push(newRoute)== and ==router.refresh()== typically the 🍞 and 🧈 of your router interactions

[Automatic and Manual Revalidation](https://www.pronextjs.dev/workshops/next-js-react-server-component-rsc-architecture-jbvxk/automatic-and-manual-revalidation-wpddq)
- automatic based on time: `export const revalidate = timeInSeconds`
- manual revalidation can be triggered via `revalidatePath()`
- "Next, we'll talk about how this full-route caching approach affects API routes."
	- okay, so the first module was last apparently

## Application Architecture Options
#+BEGIN_NOTE
Almost all of these
#+END_NOTE

[Understanding the Example Monorepo Structure](https://www.pronextjs.dev/workshops/next-js-react-server-component-rsc-architecture-jbvxk/understanding-the-example-monorepo-structure-4gpny)
- talking through the repo structure for the next couple sections
- [client-and-server/03-systems-architecture at main · ProNextJS/client-and-server](https://github.com/ProNextJS/client-and-server/tree/main/03-systems-architecture)
- includes examples for `local`, `bff`, and `external`
- couple of simulated micro services: rest, gql, or twerp script❗

[Intro to Systems Architecture](https://www.pronextjs.dev/workshops/next-js-react-server-component-rsc-architecture-jbvxk/intro-to-systems-architecture-ivz9q)
- introducing architectures
	- **local:** single client -> nextjs -> db
	- **BFF**: nextjs is backend for frontend. Client -> next -> microservices -> db
		- most common architecture when you have microservices internally
	- **External**: Client -> (nextjs -> microservices) -> db

## Local Architectures
[The API Route Variant of Local Systems](https://www.pronextjs.dev/workshops/next-js-react-server-component-rsc-architecture-jbvxk/the-api-route-variant-of-local-systems-ewm5a)
- local api INSTEAD OF using server actions
- sets up api/todo/route.ts: The route gets the todos if authed or errors
- note: seems annoying to be checking the auth separately in each of the verbs

[Building with Local Server Actions in Next.js](https://www.pronextjs.dev/workshops/next-js-react-server-component-rsc-architecture-jbvxk/building-with-local-server-actions-in-next-js-l0mn2)
- ok, same demo but using server actions instead of client side api calls

## BFF Architectures
[BFF Architecture with GraphQL](https://www.pronextjs.dev/workshops/next-js-react-server-component-rsc-architecture-jbvxk/bff-architecture-with-graph-ql-e20oo)
- this time the next app talks to a graphql api
- controlled rest api between client and next, graph between next and gql
- setting up api routes with next which translate the calls
- proxies the cookie over with `getContext`
- really good if you have a gql backend

[Backend-for-Frontend (BFF) Architecture with Server Actions](https://www.pronextjs.dev/workshops/next-js-react-server-component-rsc-architecture-jbvxk/backend-for-frontend-bff-architecture-with-server-actions-fcoc0)
- doing all the api calls to a rest endpoint from the RSC
- ⚠️ noted: seems odd to be running the fetch requests in sequence rather than parallel
- server actions make the whole thing pretty simple

[The API Variant of Backend-for-Frontend Architecture](https://www.pronextjs.dev/workshops/next-js-react-server-component-rsc-architecture-jbvxk/the-api-variant-of-backend-for-frontend-architecture-l102h)
- sets up an api route that proxies to a backend rest route
- notes that the jwt isn't encrypted, just makes the example easier
	- (stuff like this bugs me: show me how to do it properly rather than leave me with an incomplete solution)
	- afaict the complication is mostly in making sure the api server can handle the encrypted jwt that would be forwarded

[BFF Pattern with gRPC (TwirpScript)](https://www.pronextjs.dev/workshops/next-js-react-server-component-rsc-architecture-jbvxk/bff-pattern-with-g-rpc-twirp-script-qfuhk)
- (only exciting to me because of those clients I have with grpc microservices)
- not using grpc directly (a hassle to set up 😛)
- twirpscript has same rpc archicture but is easier to work with
- rpc calls in this example are between nextjs (server actions) and the "grpc server"
- synchronizing the protos through the monorepo
- (sending an unencrypted jwt through the stack again 😅)

[BFF Architecture with tRPC](https://www.pronextjs.dev/workshops/next-js-react-server-component-rsc-architecture-jbvxk/bff-architecture-with-t-rpc-ve20t)
- shows a trpc setup between client and nextjs
- callTodoService is a rest fetch call between next and backend
-
## External Architectures
[Server Architecture with an External API Domain](https://www.pronextjs.dev/workshops/next-js-react-server-component-rsc-architecture-jbvxk/server-architecture-with-an-external-api-domain-08y9s)
- local next site runs at myco.com, but talks to api.myco.com for getting data
- talks directly to api when mutating data
- api needs to webhook the next server to reset caches

[Proxying External Systems with Next.js](https://www.pronextjs.dev/workshops/next-js-react-server-component-rsc-architecture-jbvxk/proxying-external-systems-with-next-js-8vtpt)
- includes rewrites in the next config to proxy an entire endpoint to a different service
- then the client calls through api routes that transparently travel (headers and all) to that rewritten path
- it's literally bypassing the next paths and redirecting them to the proxied server _directly_
- reminds me of proxying endpoints with create react app

[Token Variation of the External Systems Architecture](https://www.pronextjs.dev/workshops/next-js-react-server-component-rsc-architecture-jbvxk/token-variation-of-the-external-systems-architecture-xgidd)
- client given a token that is used with the api
- starting with proxying the rest paths to local:5002
- storing the token on the session
- notes at the end about the token being linked to the client
	- good alternate approach is to proxy through next and store the bearer token on the next server

## Streaming and Suspense
[Intro to Suspense and Streaming in Next.js](https://www.pronextjs.dev/workshops/next-js-react-server-component-rsc-architecture-jbvxk/intro-to-suspense-and-streaming-in-next-js-wd2ud)
- 'embarrassment of riches' 😅
	- (the subs showed "next js is an embarrassment..." initially)
- previewing an app where the data (rendered on the server) takes a long time
- Use suspense to ensure the page isn't a blocking white screen
- `<Suspense fallback={...}>`

[Adding Suspense to the Application](https://www.pronextjs.dev/workshops/next-js-react-server-component-rsc-architecture-jbvxk/adding-suspense-to-the-application-e3euh)
- shows his example, working with a loading indicator, super simple
- Challenge: can we make this more granular? Load them individually?
- Gives a hint to use the react `use` hook: [use – React](https://react.dev/reference/react/use)
	- this is good! I haven't used `use` yet, but it's surprisingly straightforward
	- ❇️ you can `use(aContext)` (rather than useContext that is subject to additional rules of hooks)
	- ⚠️ ...searches upwards and does not consider context providers in the component from which you’re calling use(context).
[Granular Suspense in React](https://www.pronextjs.dev/workshops/next-js-react-server-component-rsc-architecture-jbvxk/granular-suspense-in-react-nyxhj)
- Breaking through the example:
	- removes the top level suspense and instead wraps each item in one
	- creates a sub component with the `use` hook to unwrap promises individually
- (with the `loading...` fallback it's kind of jumpy, but this would look great with skeletons)

## Advanced Topics
[DIY Streaming with Server Actions](https://www.pronextjs.dev/workshops/next-js-react-server-component-rsc-architecture-jbvxk/diy-streaming-with-server-actions-e6tx5)
- stocks example with server actions!
- makes the main dashboard into a client component that calls the server action then handles the results
- runs into an error regarding the component not being in the manifest
	- because of the way the components passed around next forgets to include it
	- shows a work around: import and maybe assign the component somewhere (even if you don't use it) just to keep it in the bundle
- end result is streaming UI: it's all one request but the first portion of the UI is sent and rendered right away
- 😕 seems odd to put the client component in the middle, but I suppose that's how you get the suspense boundary to the client first (otherwise the page is blocking)

[Cached Server Actions in Next.js](https://www.pronextjs.dev/workshops/next-js-react-server-component-rsc-architecture-jbvxk/cached-server-actions-in-next-js-ve3rl)
- 🚩 Oh no: mentions his friends at Haaretz in Isreal.
	- **This should be removed?**
	- It doesn't add anything to the content of the video, he could just say "I know a company that uses this approach" and leave the country out of it.
	- it's gonna ruffle some feathers otherwise, given the ongoing genocide by Israel
- Used it for caching portions of their content site
- using server actions for caching:
	- client component makes a server action request
	- action returns either rendered html, or client components to render
	- client component renders the content
- how server actions work:
	- client makes a post request with a special header: `Next-Action`
	- Server sees header and executes action instead of normal request
- the rest of this example includes a bunch of patching fetch, but also a new hook `useCacheableServerAction`

[File Uploads in Next.js App Router Apps](https://www.pronextjs.dev/workshops/next-js-react-server-component-rsc-architecture-jbvxk/file-uploads-in-next-js-app-router-apps-vqozo)
- going through file uploads! (ofc)
- server action example
	- using a server action for the first example: easily get the file from formdata and writes to public dir
	- uses RSC to display the picture afterward
	- (needs to revalidate the path after the file is written -- 👍🏻this is drilled into us by now I think)
- API example
	- gets the formdata / file from the post request
	- and of course, has to revalidate path again
	- the api request doesn't automatically refresh, had to also do a router.refresh()
