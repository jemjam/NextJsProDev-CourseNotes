Module three of four for [[ProNextJs.dev Course Review]]

[Next.js Production Project Setup and Infrastructure](https://www.pronextjs.dev/workshops/next-js-production-project-setup-and-infrastructure-fq4qc)
- Third module of the course
- covers a bunch of supporting elements of a production setup
- loosely includes: formatting and linting, using storybook, unit and end to end testing, and monorepos

---

## Code Quality from the Start
[Building a Strong Foundation](https://www.pronextjs.dev/workshops/next-js-production-project-setup-and-infrastructure-fq4qc/building-a-strong-foundation~5276z)
- using the analogy of having a good foundation for a house
- > "a project infrastructure template is provided in the course materials"

[Setting up ESLint and Prettier](https://www.pronextjs.dev/workshops/next-js-production-project-setup-and-infrastructure-fq4qc/setting-up-es-lint-and-prettier~dvnks)
- sets up manually
- talks about having standards set early so folks don't all do their own thing
- eslintrc includes next/core-web-vitals by default: strictest ruleset
- mentions the import order module: can be configured nicely
- putting these settings in later is painful

## Project Structure
the whole order of this module seems backwards or out of place?

[Importing Component Files](https://www.pronextjs.dev/workshops/next-js-production-project-setup-and-infrastructure-fq4qc/importing-component-files-l0juk)
- *one componet per directory*
- easy to move around
- 😕 "picking up where we left off": was this module moved up? seems to refer to tests already?

[Organizing Components into Directories](https://www.pronextjs.dev/workshops/next-js-production-project-setup-and-infrastructure-fq4qc/organizing-components-into-directories-k91el)
- this seems to come first?: showing a project with storybook and tests already configured
- calls out that the button and tests etc are all over the place

[Organizing Components into Directories](https://www.pronextjs.dev/workshops/next-js-production-project-setup-and-infrastructure-fq4qc/organizing-components-into-directories-k91el)
- Using turborepo again here: two applications
- talking about putting components close to where they're used
- showing how to add your own components when shadcn is controlling the components folder (just override the aliases)
- essentially just using a components folder
- then moves it to a different project

[Organizing Component Files](https://www.pronextjs.dev/workshops/next-js-production-project-setup-and-infrastructure-fq4qc/organizing-component-files~kgj75)
- suggests one exported component per file
- shows an example of a nested component defined inside the homepage, but it kills perf, breaks caching
- breaks each component into it's own file
- likes 50-200 line files usually (sounds good to me)
---
## Storybook
[Setting up Storybook with Next.js](https://www.pronextjs.dev/workshops/next-js-production-project-setup-and-infrastructure-fq4qc/setting-up-storybook-with-next-js-2vxd8)
- sets up storybook automatically for nextjs
- get to see how components react to prop changes

---

## Unit Testing
[Testing with Vitest](https://www.pronextjs.dev/workshops/next-js-production-project-setup-and-infrastructure-fq4qc/testing-with-vitest-u99gb)
- unit testing framework, good for components
- shows setting it up
- his pref is to have tests colocated usually
- workingn with testing library to verify a component
- vitest:ui has a nice layout to show all your test runs

[Testing Async RSCs with Vitest](https://www.pronextjs.dev/workshops/next-js-production-project-setup-and-infrastructure-fq4qc/testing-async-rscs-with-vitest-4x7uz)
- doing another example but with an async rsc this time
- await the component/page function
- there are other ways to test async pages with suspense, etc, but the basic `await component as function` is _easiest_

[Testing with Jest](https://www.pronextjs.dev/workshops/next-js-production-project-setup-and-infrastructure-fq4qc/testing-with-jest-4snaq)
- want to get tests set up with jest this time
- (calls out that you'd want to do this early)

[Testing Async RSCs with Jest](https://www.pronextjs.dev/workshops/next-js-production-project-setup-and-infrastructure-fq4qc/testing-async-rscs-with-jest-44mnl)
- not officially supported with jest yet
- same format as async with vitest: `await Page()`
- needed to add fetch mocks for the result to render
- mocking fetch isn't actually going to make the call, so also shows how to use isomorphic-fetch (to actually fetch)

## End to End Testing
[E2E Testing with Playwright](https://www.pronextjs.dev/workshops/next-js-production-project-setup-and-infrastructure-fq4qc/e2-e-testing-with-playwright-d3eyw)
- pnpm create playwright
- launches a real browser to navigate

[End-to-End Testing with Cypress](https://www.pronextjs.dev/workshops/next-js-production-project-setup-and-infrastructure-fq4qc/end-to-end-testing-with-cypress-44bpa)
- cypress ui is pretty nice

---
## Automated Quality Enforcement

[Check Bundle Size with GitHub Actions and Husky](https://www.pronextjs.dev/workshops/next-js-production-project-setup-and-infrastructure-fq4qc/check-bundle-size-with-git-hub-actions-and-husky-56f19)
- bundlewatch checks file sizes
- and husky to run it locally
- Include a file in the walkthrough, but it's not formatted right (for `.github/workflows/bundle-size.yml`)
- using material the wrong way: imports all of material just to use a button (to simulate a large page)
- calls out how bundlesize has an immense effect on perf
---
## Monorepos
[Should You Use a Monorepo?](https://www.pronextjs.dev/workshops/next-js-production-project-setup-and-infrastructure-fq4qc/should-you-use-a-monorepo-w6lx7)
- strong reasons for: shared code, multiple deployment, encapsulating business logic
- standalone packages probably don't need it, npm link is fine
- can migrate to a monorepo easily anytime

[Creating a Next.js App in a Turborepo Monorepo](https://www.pronextjs.dev/workshops/next-js-production-project-setup-and-infrastructure-fq4qc/creating-a-next-js-app-in-a-turborepo-monorepo-plp5r)
- gets set up with turborepo quick
- installs one of the boilerplates, then copies the next app into it

[Storybook in a Turborepo Monorepo](https://www.pronextjs.dev/workshops/next-js-production-project-setup-and-infrastructure-fq4qc/storybook-in-a-turborepo-monorepo-nnwqb)
- shows how to set it up three ways
	- add storybook to the ui project
	- add storybook to the nextjs project
	- add storybook as a standalone app
- shows also how to use turborepo to run storybook multiple times
---
## Advanced Component Structure
[Lego Components](https://www.pronextjs.dev/workshops/next-js-production-project-setup-and-infrastructure-fq4qc/lego-components-iwmuu)
- talking about a `client-server` repo
- share self-contained components between applications
- moves a pokemon list component into the uI library to share
- basically `microfrontends`, just not module federation at run time
- very powerful, only available to app router currently

[Naming and Organizing Server and Client Components](https://www.pronextjs.dev/workshops/next-js-production-project-setup-and-infrastructure-fq4qc/naming-and-organizing-server-and-client-components-mbtsl)
- interesting patterns have emerged over app routers lifetime (so far)
- Often have server components that couple to client components
- Some folks use the convention Component.Client.jsx or Component.Server.jsx
- adding .client or whatever doesn't include any semantic meaning in next.js (like it DOES in remix for example, where a .server component won't load on the client)

[Embrace the JS, Next.js, and React Ecosystem](https://www.pronextjs.dev/workshops/next-js-production-project-setup-and-infrastructure-fq4qc/embrace-the-js-next-js-and-react-ecosystem~6hcv6)
- hype for the vast and incredible react/next community
