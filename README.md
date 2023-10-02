<p align='center'>
    <h2 align='center'>:warning: CONCEPT UNDER DEVELOPMENT :warning:</h2>
    <h1 align='center'>React Blend</h1>
</p>

- [:world_map: Project Layout](#world_map-project-layout)
- [:dart: Goal and Guidelines](#dart-goal-and-guidelines)
  - [:leaves: Making React Cross-Platform Development a Breeze](#leaves-making-react-cross-platform-development-a-breeze)
  - [:checkered_flag: Be the Starting Point for New Projects](#checkered_flag-be-the-starting-point-for-new-projects)
  - [:vertical_traffic_light: Staying as Close to the Original Design as Possible](#vertical_traffic_light-staying-as-close-to-the-original-design-as-possible)
  - [:straight_ruler: Be Small to Always Stay Up to Date](#straight_ruler-be-small-to-always-stay-up-to-date)
  - [:arrow_up_down: Using Next.js as the Only Web Technology](#arrow_up_down-using-nextjs-as-the-only-web-technology)
  - [:bulb: Implementation Reference Sections](#bulb-implementation-reference-sections)
- [:rocket: Getting Started](#rocket-getting-started)
  - [:beginner: Creating a Minimal App](#beginner-creating-a-minimal-app)
  - [:battery: Creating a Batteries Included App](#battery-creating-a-batteries-included-app)
  - [:electric_plug: Integrating on Your Existing App](#electric_plug-integrating-on-your-existing-app)
- [:clap: Contributing](#clap-contributing)
- [:balance_scale: License](#balance_scale-license)

> **IMPORTANT TO KNOW**
>
> This project **DOES NOT SUPPORT** Next.js's Pages Router and **IS NOT TESTED** with React Navigation. [Read more](#straight_ruler-be-small-to-always-stay-up-to-date).

## :world_map: Project Layout

This repository is a monorepo that contains two projects and a sandbox development folder to be used during development.

- `📄 README.md`: Project overview (This file)
- `📁` [`packages`](/packages/): Folder containing the two projects
  - 📁 [`lib`](/packages/lib/): Library project
    - `📄 README.md`: `react-blend` documentation
    - `📁 src`: Contains the code for the Router, Image and Persistence
    - `📁 scripts`: Contains scripts to synchronize Authentication, Internationalization and Environment Variables
  - `📁` [`cli`](/packages/cli/): Command-line Interface project
    - `📄 README.md`: `create-react-blend` documentation
    - `📁 src`: `create-react-blend` code
    - `📁` [`templates`](/cli/templates/): Templates that can be used with `create-react-blend`
      - `📄 README.md`: Templates documentation
      - `📁 src`: Templates code
- `📁` [`development-sandbox`](/development-sandbox/): Minimum test environment to be used during development covering all features
  - `📁` [`apps`](/development-sandbox/apps/): Framework specific projects
    - `📁 next`: Next.js project
    - `📁 expo`: Expo project
  - `📁` [`packages`](/development-sandbox/packages/)
    - `📁 app`: Shared code and export of all packages below
    - `📁 auth`: Implements Sign In and Sign Up flows
    - `📁 navigation`: Implements all possible navigation flows
    - `📁 image`: Implements the Image component
    - `📁 i18n`: Implements several examples of internationalization
    - `📁 env-var`: Displays all environment variables
    - `📁 offline`: Implements a minimal to-do that works offline

## :dart: Goal and Guidelines

The **React Blend** is a thin layer of integration between the [Next.js](https://nextjs.org/) and [Expo](https://expo.dev/home) APIs, solving API compatibility issues and providing a unified API that works with very little interference between framework APIs. The main pain solved is not having to worry about the specifics of each framework and simply using their available APIs, it's designed in a way that you don't even notice it's there.

The macro goal of the **React Blend** is to provide a simplified and integrated development for "React Universal Apps", a concept where shared React Native code is written using together the best technologies available in the React and JavaScript ecosystems using the same codebase, always sharing as much code as possible and making code unique to only one platform explicit through architecture.

:heart: This project is heavily inspired by [Solito](https://solito.dev/), thanks a lot to your amazing work! You can also understand more about "React Universal Apps" in these projects: [create-universal-app](https://github.com/chen-rn/CUA), [create-t3-turbo](https://github.com/t3-oss/create-t3-turbo), [next-expo-solito](https://github.com/tamagui/tamagui/tree/master/starters/next-expo-solito) and [t3-turbo-and-clerk](https://github.com/clerkinc/t3-turbo-and-clerk).

The flowchart below defines how this works in practice.

```mermaid
graph LR

next-specific{{Your Next.js Specific Code and Files}}
app-router(App Router)
next-image(Next Image)
auth-js(Auth.js)
next-i18n(Next Internationalization Routing)
next-env-vars(Next Environment Variables)
workbox(Workbox)

expo-specific{{Your Expo Specific Code and Files}}
expo-router(Expo Router)
expo-image(Expo Image)
expo-auth(Expo Auth)
expo-localization(Expo Localization)
lingui-js(Lingui.js)
expo-env-vars(Expo Environment Variables)
rn-mmkv(React Native MMKV)

shared-code{{Your Shared Code}}
rb-router(React Blend Router)
rb-image(React Blend Image)
rb-auth(React Blend Auth)
rb-internationalization(React Blend Internationalization)
rb-env-vars(React Blend Environment Variables)
rb-persistence(React Blend Persistence)

subgraph Next.js Layer
    next-specific
    subgraph Next.js Packages
        app-router
        next-image
        next-i18n
        next-env-vars
    end
    auth-js
    workbox
end

subgraph Expo Layer
    expo-specific
    subgraph Expo Packages
        expo-router
        expo-image
        expo-env-vars
        expo-localization
        expo-auth
    end
    lingui-js
    rn-mmkv
end

subgraph Shared Layer
    shared-code
    subgraph React Blend
        rb-router
        rb-image
        rb-env-vars
        rb-internationalization
        rb-persistence
        rb-auth
    end
end

app-router -.- rb-router -.- expo-router
next-image -.- rb-image -.- expo-image
auth-js -.- rb-auth -.- expo-auth
next-i18n -.- rb-internationalization -.- expo-localization
rb-internationalization -.- lingui-js
next-env-vars -.- rb-env-vars -.- expo-env-vars
workbox -.- rb-persistence -.- rn-mmkv
```

### :leaves: Making React Cross-Platform Development a Breeze

Writing code that works on all platforms (Web, Android and iOS) is a difficult task, but writing code that works on all platforms using the best of your "native environments" is an even more difficult task. **React Blend** offers integrations and complete documentation to make development as easy as possible. Currently the best technologies in the ecosystem for this approach are Next.js ([React DOM](https://react.dev/)) for Web and Expo ([React Native](https://reactnative.dev/)) for Android and iOS.

> Desktop development is a more complex topic as there are two good ways to go: building Web-Based Apps with [Electron](https://www.electronjs.org/) or [Tauri](https://tauri.app/), or building Native Apps with [React Native Windows](https://github.com/microsoft/react-native-windows) and [React Native macOS](https://github.com/microsoft/react-native-macos).

> We know that [Remix](https://remix.run/) is also an excellent technology, but theoretically still little adopted. If you want to see it integrated let us know!

### :checkered_flag: Be the Starting Point for New Projects

Integrating **React Blend** into a new project can be a tedious process, plus you need to know the best packages that work fully Natively and on the Web. To make this job easier we provide a CLI that allows you to create a Batteries Included, offline-first App with several industry standard libraries. See the [Batteries Included Template documentation](/packages/cli/templates/README.md#battery-batteries-included-template) for details.

### :vertical_traffic_light: Staying as Close to the Original Design as Possible

We never intend to create new features or offer APIs that are not available in both frameworks, limiting ourselves to creating types, parameters or methods if really necessary. The whole integration rule is under the hood so you don't have to learn anything new.

### :straight_ruler: Be Small to Always Stay Up to Date

This project needs to be always up to date to work properly, so keeping things small and simple is essential to avoid falling into trouble. Unfortunately this meant that things had to be cut back and it was decided to **drop support for Next.js's Pages Router and React Navigation**, focusing all resources on integrating Next.js's App Router and Expo Router APIs. This situation may change in the future, let us know!

### :arrow_up_down: Using Next.js as the Only Web Technology

Despite being often seen as a framework for Hybrid Mobile Development, Expo positions itself as a framwork for "Universal Native Apps with React That Run on Android, iOS, and the Web". This means that more and more of its packages provide full support for the Web, dispensing with the integration of another technology such as Next.js. However, resources are scarce and Expo's main focus is on Native Apps, at the moment offering only basic web resources, so it's important to use Next.js exclusively for building more optimized and modern Web Applications.

### :bulb: Implementation Reference Sections

Each section of the documentation can have a hidden section at the end called "Implementation Reference", responsible for gathering all the information necessary to demonstrate the use and differences between the frameworks, as well as mapping possible new additions that need to be made for full integration. You don't have to worry about it, it's just for curious people and developers of this package.

## :rocket: Getting Started

> **TIP**
>
> You can see the templates details in the [templates documentation](/packages/cli/templates/). After creating or configuring your project, [go to the documentation](/packages/lib/) and start coding!

### :beginner: Creating a Minimal App

###### yarn

```shell
yarn create react-blend@latest --create my-awesome-app
```

###### npm

```shell
npx create-react-blend@latest --create my-awesome-app
```

### :battery: Creating a Batteries Included App

###### yarn

```shell
yarn create react-blend@latest --create my-awesome-app --template with-batteries-included
```

###### npm

```shell
npx create-react-blend@latest --create my-awesome-app --template with-batteries-included
```

### :electric_plug: Integrating on Your Existing App

###### yarn

```shell
yarn add react-blend@latest
```

###### npm

```shell
npm install react-blend@latest
```

## :clap: Contributing

If you like **React Blend** and want to help make it better, just open an issue or discussion in this repository.

## :balance_scale: License

The **React Blend** source code is made available under the [MIT license](LICENSE).
