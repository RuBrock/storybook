# Storybook

## CES Info

### Group Members

| Student               | ID        |
| --------------------- | --------- |
| Beatriz Oziel de Lima | 202510621 |
| Rubens Brock Silva    | 202510624 |
| Matvii Suk            | 202514197 |

## How alive is the project?

Storybook is an extremely active open-source project and remains the industry standard for UI component development. It has an active contributor community, frequent releases, ongoing feature improvements, and strong adoption across both startups and large technology companies.

<img width="689" height="339" alt="Screenshot from 2026-05-13 15-37-21" src="https://github.com/user-attachments/assets/47288415-19e7-482f-b26c-fd1d8aef338a" />

## How important is it?

In modern frontend development, Storybook is considered one of the most important tools in a developer's workflow, alongside frontend frameworks such as React, Angular, or Vue, and package managers like npm or pnpm.

It is used in production by major companies such as:

- Pinterest
- Vimeo
- Mailchimp
- Target
- GitHub
- Airbnb
- Dropbox

Its adoption demonstrates its importance in building scalable design systems and maintainable frontend applications.

## What is it good for?

Storybook allows developers to build and test UI components independently from the main application.

Its main benefits include:

- **Component Isolation** – Build components like buttons, forms, modals, and layouts without running the entire application.
- **Visual Documentation** – Each component state is documented as a "story", making the UI easier to understand and maintain.
- **Collaboration** – Designers, developers, and QA engineers can review components in a shared environment.
- **Testing** – Supports visual regression testing, interaction testing, and accessibility testing.
- **Reusability** – Helps teams create scalable and reusable design systems.

Overall, Storybook improves development speed, consistency, and code quality in frontend projects.

## Technologies Involved

Storybook integrates with modern frontend technologies, including:

### Frameworks

- React
- Vue.js
- Angular
- Svelte

### Languages

- JavaScript
- TypeScript

### Build Tools

- Webpack
- Vite

### Testing & Styling Ecosystem

- Jest
- Testing Library
- CSS Modules
- Styled Components
- Tailwind CSS

This broad ecosystem support makes Storybook highly flexible for different frontend architectures.

## Issues

| Issue                                                           | Resources                           |
| --------------------------------------------------------------- | ----------------------------------- |
| [#34258](https://github.com/storybookjs/storybook/issues/34258) | [Report doc](issue-34258-report.md) |
| [#34566](https://github.com/storybookjs/storybook/issues/34566) | [Report doc](issue-34566-report.md) |
| [#21524](https://github.com/storybookjs/storybook/issues/21524) | [Report doc](issue-21524-report.md) |

## Project Maintainability Status

Working on the three issues gave us a decent view into how maintainable Storybook actually is in practice. Overall impression: it's a well-run project, but it's also very large, and that scale creates blind spots.

| Artefact                       | Rating | Notes                                                                                                                                                                                                                                                                                             |
| ------------------------------ | ------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Documentation                  | A      | CONTRIBUTING.md is thorough. The main gap we hit is that TypeScript types can lag behind runtime behavior. Issue [#21524](issue-21524-report.md) is a clear example of that.                                                                                                                      |
| Source code quality            | B      | The code is clean and well-structured. That said, identical patterns quietly spread across six framework packages without anyone noticing ([#34258](issue-34258-report.md)). The architecture is sound, but at this scale some duplication slips through.                                         |
| Error handling / observability | C      | Generic catch-all error buckets make debugging harder than it needs to be. Issue [#34566](issue-34566-report.md) showed that a real, categorizable failure was being swallowed by `UncaughtManagerError`. The infrastructure to fix it was already there, it just wasn't being used consistently. |
| Community support              | A      | Maintainers respond quickly, issues are well-labeled, and the Discord is active. Finding a "good first issue" to work on was kind of straightforward, and PR feedback came fast.                                                                                                                  |
| Architecture                   | B      | The renderer/builder/framework separation is clean and NX manages task dependencies well. The monorepo structure makes sense for a project this size. The downside is that cross-package patterns can diverge without any tooling catching it.                                                    |

### Concrete improvement suggestions

**Types:** Run a periodic audit comparing public type signatures against integration tests or runtime behavior. Issue [#21524](issue-21524-report.md) could have been caught by a test that actually exercises the async path through TypeScript's compiler.

**Error handling:** Add a lint rule or architectural review step to flag plain `TypeError` throws in manager-side code. The `StorybookError` base class exists, it should be the default, not the exception.

**Cross-package duplication:** The `createCorePreset` factory we introduced in [#34258](issue-34258-report.md) is a step in the right direction, but there's no automated check that prevents the old pattern from coming back in new framework packages. A custom ESLint rule or a structural test would help enforce the pattern going forward.

**Documentation:** Version-stamp the more complex behavioral docs (like how async story resolvers work). Type definitions that diverge from runtime docs are easy to miss during a code review.

---

## Rest of the Original README

<p align="center">
  <a href="https://storybook.js.org/?ref=readme">
    <picture>
      <source media="(prefers-color-scheme: dark)" srcset="https://user-images.githubusercontent.com/263385/199832481-bbbf5961-6a26-481d-8224-51258cce9b33.png">
      <img src="https://user-images.githubusercontent.com/321738/63501763-88dbf600-c4cc-11e9-96cd-94adadc2fd72.png" alt="Storybook" width="400" />
    </picture>
    
  </a>
  
</p>

<p align="center">Build bulletproof UI components faster</p>

<br/>

<p align="center">
  <a href="https://circleci.com/gh/storybookjs/storybook">
    <img src="https://circleci.com/gh/storybookjs/storybook.svg?style=shield" alt="Build Status on CircleCI" />
  </a>
  <a href="https://codecov.io/gh/storybookjs/storybook">
    <img src="https://codecov.io/gh/storybookjs/storybook/branch/main/graph/badge.svg" alt="codecov" />
  </a>
  <a href="https://github.com/storybookjs/storybook/blob/main/LICENSE">
    <img src="https://img.shields.io/github/license/storybookjs/storybook.svg" alt="License" />
  </a>
  <br/>
  <a href="https://discord.gg/storybook">
    <img src="https://img.shields.io/badge/discord-join-7289DA.svg?logo=discord&longCache=true&style=flat" />
  </a>
  <a href="https://storybook.js.org/community/?ref=readme">
    <img src="https://img.shields.io/badge/community-join-4BC424.svg" alt="Storybook Community" />
  </a>
  <a href="#backers">
    <img src="https://opencollective.com/storybook/backers/badge.svg" alt="Backers on Open Collective" />
  </a>
  <a href="#sponsors">
    <img src="https://opencollective.com/storybook/tiers/sponsors/badge.svg" alt="Sponsors on Open Collective" />
  </a>
  <a href="https://x.com/intent/follow?screen_name=storybookjs">
    <img src="https://img.shields.io/twitter/follow/storybookjs?color=blue&logo=twitter" alt="Official Twitter Handle" />
  </a>
  <a href="https://api.securityscorecards.dev/projects/github.com/storybookjs/storybook">
    <img src="https://api.securityscorecards.dev/projects/github.com/storybookjs/storybook/badge" alt="OpenSSF Scorecard"/>
  </a>
</p>

<p align="center">
Storybook is a frontend workshop for building UI components and pages in isolation. Thousands of teams use it for UI development, testing, and documentation. Find out more at <a href="https://storybook.js.org/?ref=readme">storybook.js.org</a>!
</p>

<center>
  <img src="https://raw.githubusercontent.com/storybookjs/storybook/refs/heads/release-6-5/media/storybook-intro.gif" width="100%" />
</center>

<p align="center">
  View README for:<br/>
  <a href="https://github.com/storybookjs/storybook/blob/main/README.md" title="latest"><img alt="latest" src="https://img.shields.io/npm/v/@storybook/react/latest?style=for-the-badge&logo=storybook&logoColor=ffffff&color=66BF3C" /></a>
  <a href="https://github.com/storybookjs/storybook/blob/next/README.md" title="next"><img alt="next" src="https://img.shields.io/npm/v/@storybook/react/next?style=for-the-badge&logo=storybook&logoColor=ffffff&color=1EA7FD" /></a>
</p>

## Table of contents

- 🚀 [Getting Started](#getting-started)
- 📒 [Projects](#projects)
  - 🛠 [Supported Frameworks & Examples](#supported-frameworks)
  - 🔗[Addons](#addons)
- 🏅 [Badges & Presentation materials](#badges--presentation-materials)
- 👥 [Community](#community)
- 👏 [Contributing](#contributing)
  - 👨‍💻 [Development scripts](#development-scripts)
  - 💸 [Sponsors](#sponsors)
  - 💵 [Backers](#backers)
- :memo: [License](#license)

## Getting Started

Visit [Storybook's website](https://storybook.js.org/?ref=readme) to learn more about Storybook and to get started.

### Documentation

Documentation can be found on [Storybook's docs site](https://storybook.js.org/docs?ref=readme).

### Examples

View [Component Encyclopedia](https://storybook.js.org/showcase?ref=readme) to see how leading teams use Storybook.

Use [storybook.new](https://storybook.new) to quickly create an example project in Stackblitz.

Storybook comes with a lot of [addons](https://storybook.js.org/docs/configure/user-interface/storybook-addons?ref=readme) for component design, documentation, testing, interactivity, and so on. Storybook's API makes it possible to configure and extend in various ways. It has even been extended to support React Native, Android, iOS, and Flutter development for mobile.

### Community

For additional help, share your issue in [the repo's GitHub Discussions](https://github.com/storybookjs/storybook/discussions/new?category=help).

## Projects

### Supported Frameworks

| Renderer                                                       | Demo                                                                                                                                                                         |                                                                                                                                                       |
| -------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------- |
| [React](code/renderers/react)                                  | [![Storybook demo](https://img.shields.io/npm/v/@storybook/react/latest?style=flat-square&color=blue&label)](https://next--630511d655df72125520f051.chromatic.com/)          | [![React](https://img.shields.io/npm/dm/@storybook/react?style=flat-square&color=eee)](code/renderers/react)                                          |
| [Angular](code/frameworks/angular/)                            | [![Storybook demo](https://img.shields.io/npm/v/@storybook/angular/latest?style=flat-square&color=blue&label)](https://next--6322ce6af69825592bbb28fc.chromatic.com/)        | [![Angular](https://img.shields.io/npm/dm/@storybook/angular?style=flat-square&color=eee)](code/frameworks/angular/)                                  |
| [Vue 3](code/renderers/vue3)                                   | [![Storybook demo](https://img.shields.io/npm/v/@storybook/vue3/latest?style=flat-square&color=blue&label)](https://next--630513346a8e284ae244d415.chromatic.com/)           | [![Vue 3](https://img.shields.io/npm/dm/@storybook/vue3?style=flat-square&color=eee)](code/renderers/vue3/)                                           |
| [Web components](code/renderers/web-components)                | [![Storybook demo](https://img.shields.io/npm/v/@storybook/web-components/latest?style=flat-square&color=blue&label)](https://next--638db5bf49adfdfe8cf545e0.chromatic.com/) | [![Svelte](https://img.shields.io/npm/dm/@storybook/web-components?style=flat-square&color=eee)](code/renderers/web-components)                       |
| [React Native](https://github.com/storybookjs/react-native)    | [![](https://img.shields.io/npm/v/@storybook/react-native/latest?style=flat-square&color=blue&label)](/)                                                                     | [![React Native](https://img.shields.io/npm/dm/@storybook/react-native?style=flat-square&color=eee)](https://github.com/storybookjs/react-native)     |
| [HTML](code/renderers/html)                                    | [![Storybook demo](https://img.shields.io/npm/v/@storybook/html/latest?style=flat-square&color=blue&label)](https://next--63dd39a158cf6fc05199b4bb.chromatic.com/)           | [![HTML](https://img.shields.io/npm/dm/@storybook/html?style=flat-square&color=eee)](code/renderers/html)                                             |
| [Ember](code/frameworks/ember/)                                | [![](https://img.shields.io/npm/v/@storybook/ember/latest?style=flat-square&color=blue&label)](/)                                                                            | [![Ember](https://img.shields.io/npm/dm/@storybook/ember?style=flat-square&color=eee)](code/frameworks/ember/)                                        |
| [Svelte](code/renderers/svelte)                                | [![Storybook demo](https://img.shields.io/npm/v/@storybook/svelte/latest?style=flat-square&color=blue&label)](https://next--630873996e4e3557791c069c.chromatic.com/)         | [![Svelte](https://img.shields.io/npm/dm/@storybook/svelte?style=flat-square&color=eee)](code/renderers/svelte)                                       |
| [Preact](code/renderers/preact)                                | [![Storybook demo](https://img.shields.io/npm/v/@storybook/preact/latest?style=flat-square&color=blue&label)](https://next--63b588a512565bfaace15e7c.chromatic.com/)         | [![Preact](https://img.shields.io/npm/dm/@storybook/preact?style=flat-square&color=eee)](code/renderers/preact)                                       |
| [Qwik](https://github.com/literalpie/storybook-framework-qwik) | [![](https://img.shields.io/npm/v/storybook-framework-qwik/latest?style=flat-square&color=blue&label)](/)                                                                    | [![Qwik](https://img.shields.io/npm/dm/storybook-framework-qwik?style=flat-square&color=eee)](https://github.com/literalpie/storybook-framework-qwik) |
| [SolidJS](https://github.com/solidjs-community/storybook)      | [![](https://img.shields.io/npm/v/storybook-solidjs-vite/latest?style=flat-square&color=blue&label)](/)                                                                      | [![SolidJS](https://img.shields.io/npm/dm/storybook-solidjs-vite?style=flat-square&color=eee)](https://github.com/solidjs-community/storybook)        |
| [Android, iOS, Flutter](https://github.com/storybookjs/native) | [![](https://img.shields.io/npm/v/@storybook/native/latest?style=flat-square&color=blue&label)](/)                                                                           | [![Native](https://img.shields.io/npm/dm/@storybook/native?style=flat-square&color=eee)](https://github.com/storybookjs/native)                       |

### Addons

| Addons                                                                    |                                                                            |
| ------------------------------------------------------------------------- | -------------------------------------------------------------------------- |
| [a11y](code/addons/a11y/)                                                 | Test components for user accessibility in Storybook                        |
| [actions](code/core/src/actions/)                                         | Log actions as users interact with components in the Storybook UI          |
| [backgrounds](code/core/src/backgrounds)                                  | Let users choose backgrounds in the Storybook UI                           |
| [cssresources](https://github.com/storybookjs/addon-cssresources)         | Dynamically add/remove CSS resources to the component iframe               |
| [design assets](https://github.com/storybookjs/addon-design-assets)       | View images, videos, and weblinks alongside your story                     |
| [docs](code/addons/docs/)                                                 | Add high quality documentation to your components                          |
| [events](https://github.com/storybookjs/addon-events)                     | Interactively fire events to components that respond to EventEmitter       |
| [google-analytics](https://github.com/storybookjs/addon-google-analytics) | Reports google analytics on stories                                        |
| [graphql](https://github.com/storybookjs/addon-graphql)                   | Query a GraphQL server within Storybook stories                            |
| [jest](https://github.com/storybookjs/addon-jest)                         | View the results of components' unit tests in Storybook                    |
| [links](code/addons/links/)                                               | Create links between stories                                               |
| [measure](code/core/src/measure/)                                         | Visually inspect the layout and box model within the Storybook UI          |
| [outline](code/core/src/outline/)                                         | Visually debug the CSS layout and alignment within the Storybook UI        |
| [query params](https://github.com/storybookjs/addon-queryparams)          | Mock query params                                                          |
| [viewport](code/core/src/viewport/)                                       | Change display sizes and layouts for responsive components using Storybook |

See [Addon / Framework Support Table](https://storybook.js.org/docs/configure/integration/frameworks-feature-support?ref=readme)

To continue improving your experience, we have to eventually deprecate or remove certain addons in favor of new and better tools.

If you're using info/notes, we highly recommend you migrate to [docs](code/addons/docs/) instead, and [here is a guide](code/addons/docs/docs/recipes.md#migrating-from-notesinfo-addons) to help you.

If you're using contexts, we highly recommend you migrate to [toolbars](https://github.com/storybookjs/storybook/tree/next/code/addons/toolbars) and [here is a guide](https://github.com/storybookjs/storybook/blob/next/MIGRATION.md#deprecated-addon-contexts) to help you.

If you're using addon-storyshots, we highly recommend you migrate to the Storybook [test-runner](https://github.com/storybookjs/test-runner) and [here is a guide](https://storybook.js.org/docs/writing-tests/storyshots-migration-guide?ref=readme) to help you.

## Badges & Presentation materials

We have a badge! Link it to your live Storybook example.

![Storybook](https://cdn.jsdelivr.net/gh/storybookjs/brand@main/badge/badge-storybook.svg)

```md
[![Storybook](https://cdn.jsdelivr.net/gh/storybookjs/brand@main/badge/badge-storybook.svg)](link to site)
```

If you're looking for material to use in your Storybook presentation, such as logos, video material, and the colors we use, you can find it all on our [brand repo](https://github.com/storybookjs/brand).

## Community

- Tweeting via [@storybookjs](https://x.com/storybookjs)
- Blogging at [storybook.js.org](https://storybook.js.org/blog/?ref=readme) and [Medium](https://medium.com/storybookjs)
- Chatting on [Discord](https://discord.gg/storybook)
- Videos and streams at [YouTube](https://www.youtube.com/channel/UCr7Quur3eIyA_oe8FNYexfg)

## Contributing

Contributions to Storybook are always welcome!

- 📥 Pull requests and 🌟 Stars are always welcome.
- Read our [contributing guide](CONTRIBUTING.md) to get started,
  or find us on [Discord](https://discord.gg/storybook), we will take the time to guide you.

Looking for a first issue to tackle?

- We tag issues with [![Good First Issue](https://img.shields.io/github/issues/storybookjs/storybook/good%20first%20issue.svg)](https://github.com/storybookjs/storybook/issues?q=is%3Aopen+is%3Aissue+label%3A%22good+first+issue%22) when we think they are well suited for people who are new to the codebase or OSS in general.
- [Talk to us](https://discord.gg/storybook), we'll find something that suits your skills and learning interests.

### Development scripts

Storybook is organized as a monorepo. Useful scripts include:

#### `yarn start`

> Runs a sandbox template storybook with test stories

#### `yarn task`

> As above, but gives you options to customize the sandbox (e.g. selecting other frameworks)

#### `yarn lint`

> boolean check if code conforms to linting rules - uses remark & eslint

- `yarn lint:js` - will check js
- `yarn lint:md` - will check markdown + code samples
- `yarn lint:js --fix` - will automatically fix js

#### `yarn test`

> boolean check if unit tests all pass - uses jest

- `yarn run test --core --watch` - will run core tests in watch-mode

### Sponsors

Become a sponsor to have your logo and website URL on our README on Github. \[[Become a sponsor](https://opencollective.com/storybook#sponsor)]

<a href="https://opencollective.com/storybook/tiers/sponsors/0/website?requireActive=true" target="_blank"><img src="https://opencollective.com/storybook/tiers/sponsors/0/avatar.svg?requireActive=true"></a>
<a href="https://opencollective.com/storybook/tiers/sponsors/1/website?requireActive=true" target="_blank"><img src="https://opencollective.com/storybook/tiers/sponsors/1/avatar.svg?requireActive=true"></a>
<a href="https://opencollective.com/storybook/tiers/sponsors/2/website?requireActive=true" target="_blank"><img src="https://opencollective.com/storybook/tiers/sponsors/2/avatar.svg?requireActive=true"></a>
<a href="https://opencollective.com/storybook/tiers/sponsors/3/website?requireActive=true" target="_blank"><img src="https://opencollective.com/storybook/tiers/sponsors/3/avatar.svg?requireActive=true"></a>
<a href="https://opencollective.com/storybook/tiers/sponsors/4/website?requireActive=true" target="_blank"><img src="https://opencollective.com/storybook/tiers/sponsors/4/avatar.svg?requireActive=true"></a>
<a href="https://opencollective.com/storybook/tiers/sponsors/5/website?requireActive=true" target="_blank"><img src="https://opencollective.com/storybook/tiers/sponsors/5/avatar.svg?requireActive=true"></a>
<a href="https://opencollective.com/storybook/tiers/sponsors/6/website?requireActive=true" target="_blank"><img src="https://opencollective.com/storybook/tiers/sponsors/6/avatar.svg?requireActive=true"></a>
<a href="https://opencollective.com/storybook/tiers/sponsors/7/website?requireActive=true" target="_blank"><img src="https://opencollective.com/storybook/tiers/sponsors/7/avatar.svg?requireActive=true"></a>
<a href="https://opencollective.com/storybook/tiers/sponsors/8/website?requireActive=true" target="_blank"><img src="https://opencollective.com/storybook/tiers/sponsors/8/avatar.svg?requireActive=true"></a>
<a href="https://opencollective.com/storybook/tiers/sponsors/9/website?requireActive=true" target="_blank"><img src="https://opencollective.com/storybook/tiers/sponsors/9/avatar.svg?requireActive=true"></a>
<a href="https://opencollective.com/storybook/tiers/sponsors/10/website?requireActive=true" target="_blank"><img src="https://opencollective.com/storybook/tiers/sponsors/10/avatar.svg?requireActive=true"></a>
<a href="https://opencollective.com/storybook/tiers/sponsors/11/website?requireActive=true" target="_blank"><img src="https://opencollective.com/storybook/tiers/sponsors/11/avatar.svg?requireActive=true"></a>
<a href="https://opencollective.com/storybook/tiers/sponsors/12/website?requireActive=true" target="_blank"><img src="https://opencollective.com/storybook/tiers/sponsors/12/avatar.svg?requireActive=true"></a>
<a href="https://opencollective.com/storybook/tiers/sponsors/13/website?requireActive=true" target="_blank"><img src="https://opencollective.com/storybook/tiers/sponsors/13/avatar.svg?requireActive=true"></a>
<a href="https://opencollective.com/storybook/tiers/sponsors/14/website?requireActive=true" target="_blank"><img src="https://opencollective.com/storybook/tiers/sponsors/14/avatar.svg?requireActive=true"></a>
<a href="https://opencollective.com/storybook/tiers/sponsors/15/website?requireActive=true" target="_blank"><img src="https://opencollective.com/storybook/tiers/sponsors/15/avatar.svg?requireActive=true"></a>
<a href="https://opencollective.com/storybook/tiers/sponsors/16/website?requireActive=true" target="_blank"><img src="https://opencollective.com/storybook/tiers/sponsors/16/avatar.svg?requireActive=true"></a>
<a href="https://opencollective.com/storybook/tiers/sponsors/17/website?requireActive=true" target="_blank"><img src="https://opencollective.com/storybook/tiers/sponsors/17/avatar.svg?requireActive=true"></a>
<a href="https://opencollective.com/storybook/tiers/sponsors/18/website?requireActive=true" target="_blank"><img src="https://opencollective.com/storybook/tiers/sponsors/18/avatar.svg?requireActive=true"></a>
<a href="https://opencollective.com/storybook/tiers/sponsors/19/website?requireActive=true" target="_blank"><img src="https://opencollective.com/storybook/tiers/sponsors/19/avatar.svg?requireActive=true"></a>
<a href="https://opencollective.com/storybook/tiers/sponsors/20/website?requireActive=true" target="_blank"><img src="https://opencollective.com/storybook/tiers/sponsors/20/avatar.svg?requireActive=true"></a>
<a href="https://opencollective.com/storybook/tiers/sponsors/21/website?requireActive=true" target="_blank"><img src="https://opencollective.com/storybook/tiers/sponsors/21/avatar.svg?requireActive=true"></a>
<a href="https://opencollective.com/storybook/tiers/sponsors/22/website?requireActive=true" target="_blank"><img src="https://opencollective.com/storybook/tiers/sponsors/22/avatar.svg?requireActive=true"></a>
<a href="https://opencollective.com/storybook/tiers/sponsors/23/website?requireActive=true" target="_blank"><img src="https://opencollective.com/storybook/tiers/sponsors/23/avatar.svg?requireActive=true"></a>
<a href="https://opencollective.com/storybook/tiers/sponsors/24/website?requireActive=true" target="_blank"><img src="https://opencollective.com/storybook/tiers/sponsors/24/avatar.svg?requireActive=true"></a>
<a href="https://opencollective.com/storybook/tiers/sponsors/25/website?requireActive=true" target="_blank"><img src="https://opencollective.com/storybook/tiers/sponsors/25/avatar.svg?requireActive=true"></a>

### Backers

By making a recurring donation, you can support us and our work. \[[Become a backer](https://opencollective.com/storybook#backer)]

<a href="https://opencollective.com/storybook"><img src="https://opencollective.com/storybook/tiers/backers.svg?limit=80&button=false&avatarHeight=46&width=750"></a>

## License

[MIT](https://github.com/storybookjs/storybook/blob/main/LICENSE)

-the end-
