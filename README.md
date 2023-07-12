<p align='center'>
    <h1 align='center'>React Universal Layer</h1>
</p>
<p align='center'>
  <a aria-label='Join our Discord' href='' target='_blank'>
    <img alt='Discord' src='https://img.shields.io/discord/695411232856997968.svg?style=flat-square&labelColor=000000&color=4630EB&logo=discord&logoColor=FFFFFF&label=' />
  </a>
  <a aria-label='React Universal Layer is free to use' href='' target='_blank'>
    <img alt='License: MIT' src='https://img.shields.io/badge/License-MIT-success.svg?style=flat-square&color=33CC12' target='_blank' />
  </a>
</p>

---

- [📍 Goal and Guidelines](#-goal-and-guidelines)
  - [🍃 Making Cross-Platform Development a Breeze](#-making-cross-platform-development-a-breeze)
  - [🏁 Be the Starting Point for New Projects](#-be-the-starting-point-for-new-projects)
  - [🚦 Staying as Close to the Original Design as Possible](#-staying-as-close-to-the-original-design-as-possible)
  - [📏 Be Small to Always Stay Up to Date](#-be-small-to-always-stay-up-to-date)
  - [🌐 Using Next.js as the Only Web Technology](#-using-nextjs-as-the-only-web-technology)
  - [💡 Implementation Reference Sections](#-implementation-reference-sections)
- [🚀 Getting Started](#-getting-started)
  - [Creating a Minimal App](#creating-a-minimal-app)
  - [🌟 Creating a Batteries Included App](#-creating-a-batteries-included-app)
  - [Installing on Your Existing App](#installing-on-your-existing-app)
- [📚 Documentation](#-documentation)
  - [Instalation](#instalation)
  - [🗄️ Roles of Files and Folders](#️-roles-of-files-and-folders)
    - [Important Rules](#important-rules)
    - [Files Roles](#files-roles)
    - [Folders Roles](#folders-roles)
  - [⛖ Linking and Navigating](#-linking-and-navigating)
    - [Navigation with `<Link>` Component](#navigation-with-link-component)
    - [Imperative Navigation with `router`](#imperative-navigation-with-router)
    - [Get Param(s) Sent Throug Route](#get-params-sent-throug-route)
  - [🖼️ `<Image />` Component](#️-image--component)
  - [🔑 Authentication](#-authentication)
- [👏 Contributing](#-contributing)
- [⚖️ License](#️-license)

## 📍 Goal and Guidelines

```mermaid
graph LR

next-specific{{Your Next.js Specific Code and Files}}
app-router(App Router)
next-image(Next Image Component)
next-auth(Next Auth)

expo-specific{{Your Expo Specific Code and Files}}
expo-router(Expo Router)
expo-image(Expo Image Component)
expo-auth(Expo Auth)

shared-code{{Your Shared Code}}
rul-router(Universal Router)    
rul-image(Universal Image Component)    
rul-auth(Universal Auth)

subgraph Next.js Layer
    next-specific
    subgraph Next.js Packages
        app-router 
        next-image 
        next-auth
    end
end

subgraph Expo Layer
    expo-specific
    subgraph Expo Packages
        expo-router 
        expo-image
        expo-auth
    end
end

subgraph Shared Layer
    shared-code
    subgraph React Universal Layer
        rul-router 
        rul-image 
        rul-auth
    end 
end

app-router <-. integrates .-> rul-router <-. integrates .-> app-router
next-image <-. integrates .-> rul-image <-. integrates .-> expo-image
next-auth <-. integrates .-> rul-auth <-. integrates .-> expo-auth
```

The **React Universal Layer** is a thin layer of integration between the [Next.js](https://nextjs.org/) and [Expo](https://expo.dev/home) APIs, solving API compatibility issues and providing a unified API that works with very little interference between framework APIs. The main pain solved is not having to worry about the specifics of each framework and simply using their available APIs, it's designed in a way that you don't even notice it's there.

❤️ This project is heavily inspired by [Solito](https://solito.dev/), thanks a lot to your amazing work!

### 🍃 Making Cross-Platform Development a Breeze

Writing code that works on all platforms (Web, Android, iOS, Desktop) is a difficult task, but writing code that works on all platforms using the best of their native environments is an even harder task. This is the main objective of 'React Universal Apps', the idea of writing React code that uses the best and most modern development, which currently boils down to Expo ([React Native](https://reactnative.dev/)) for Android and iOS, and Next.js ([React DOM](https://react.dev/)) for Web. Desktop development is a more complex topic as there are two good ways to go: building web-based apps with [Electron](https://www.electronjs.org/) or [Tauri](https://tauri.app/), or building native apps with [React Native Windows](https://github.com/microsoft/react-native-windows) and [React Native macOS](https://github.com/microsoft/react-native-macos).

### 🏁 Be the Starting Point for New Projects

Integrating React Native Layer into a new project can be a tedious process, plus you need to know the best packages that work fully Natively and on the Web. To make this job easier we provide a CLI that allows you to create a Batteries Included, offline-first App with [Tamagui](https://tamagui.dev/), [TanStack Query](https://tanstack.com/query/latest), [Zustand](https://zustand-demo.pmnd.rs/), [React Native MMKV](https://github.com/mrousavy/react-native-mmkv) and [ESLint](https://eslint.org/).

### 🚦 Staying as Close to the Original Design as Possible

We never intend to create new features or offer APIs that are not available in both frameworks, limiting ourselves to creating types, parameters or methods if really necessary. The whole integration rule is under the hood so you don't have to learn anything new.

### 📏 Be Small to Always Stay Up to Date

This project needs to be always up to date to work properly, so keeping things small and simple is essential to avoid falling into trouble. Unfortunately this meant that things had to be cut back and it was decided to **drop support for Next.js's Pages Router and React Navigation**, focusing all resources on integrating Next.js's App Router and Expo Router APIs. This situation may change in the future, let us know!

### 🌐 Using Next.js as the Only Web Technology

Despite being often seen as a framework for hybrid mobile development, Expo positions itself as a framwork for 'Universal Native Apps with React That Run on Android, iOS, and the Web'. This means that more and more of its packages provide full support for the Web, dispensing with the integration of another technology such as Next.js. However, resources are scarce and Expo's main focus is on native, at the moment offering only basic web resources, so it's important to use Next.js exclusively for building more optimized and modern Web Applications.

### 💡 Implementation Reference Sections

Each section of the documentation can have a hidden section at the end called 'Implementation Reference', responsible for gathering all the information necessary to demonstrate the use and differences between the frameworks, as well as mapping possible new additions that need to be made for full integration. You don't have to worry about it, it's just for curious people and developers of this package.

## 🚀 Getting Started

### Creating a Minimal App

```shell
npx create-universal-layer-app@latest
```

### 🌟 Creating a Batteries Included App

```shell
npx create-universal-layer-app@latest --template with-batteries-included
```

### Installing on Your Existing App

###### npm

```shell
npm install react-universal-layer@latest
```

###### yarn

```shell
yarn add react-universal-layer@latest
```

## 📚 Documentation

### Instalation

### 🗄️ Roles of Files and Folders

There is nothing new here, this section of the documentation has the sole purpose of succinctly summarizing and keeping track of all folder and file scenarios possible to implement in each framework.

- ✅ Role supported for the framework.
- ❌ Role not supported for the framework.

#### Important Rules

##### App Router Requires a Root Layout

App Router requires a root `📄 layout.js` defined in `📁 app`. Expo Router does not require.

##### Using Your Own Files Inside Routers

#### Files Roles

##### Page File

##### Layout File

##### Loading File

##### Not Found File

##### Error File

##### Global Error File

##### Template File

##### Default File

#### Folders Roles

##### Root Route

Matches route `/`.

###### ✅ App Router

```
├── 📁 app
    ├── 📄 layout.js
    ├── 📄 page.js
```

###### ✅ Expo Router

```
├── 📁 app
    ├── 📄 index.js
```

##### Named Routes

Matches route `/route-name`.

###### ✅ App Router

```
├── 📁 app
    ├── 📄 layout.js
    ├── 📁 route-name
        ├── 📄 page.js
```

###### ✅ Expo Router

```
├── 📁 app
    ├── 📄 route-name.js
```

```
├── 📁 app
    ├── 📁 route-name
        ├── 📄 index.js
```

##### Nested Routes

Matches route `/parent-route-name/child-route-name`.

###### ✅ App Router

```
├── 📁 app
    ├── 📄 layout.js
    ├── 📁 parent-route-name
        ├── 📁 child-route-name
            ├── 📄 page.js
```

###### ✅ Expo Router

```
├── 📁 app
    ├── 📁 parent-route-name
        ├── 📄 child-route-name
```

```
├── 📁 app
    ├── 📁 parent-route-name
        ├── 📁 child-route-name
            ├── 📄 index.js
```

##### Dynamic Route with One Parameter

Matches route `/route-name/[param]` where `📁 [param]` is a single value sent by the route.

###### ✅ App Router

```
├── 📁 app
    ├── 📄 layout.js
    ├── 📁 route-name
        ├── 📁 [param]
            ├── 📄 page.js
```

###### ✅ Expo Router

```
├── 📁 app
    ├── 📁 route-name
        ├── 📄 [param].js
```

```
├── 📁 app
    ├── 📁 route-name
        ├── 📁 [param]
            ├── 📄 index.js
```

##### Dynamic Route with Multiple Parameters

Matches route `/route-name/[...params]` where `📁 [...params]` is a array of values sent by the route.

###### ✅ App Router

Navigating to `/route-name` throws an error. To get this behavior you need to use [Multiple Optional Parameters](#dynamic-route-with-multiple-optional-parameters).

```
├── 📁 app
    ├── 📄 layout.js
    ├── 📁 route-name
        ├── 📁 [...params]
            ├── 📄 page.js
```

###### ✅ Expo Router

```
├── 📁 app
    ├── 📁 route-name
        ├── 📄 [...params].js
```

```
├── 📁 app
    ├── 📁 route-name
        ├── 📁 [...params]
            ├── 📄 index.js
```

##### Dynamic Route with Multiple Optional Parameters

Matches route `/route-name/[[...params]]` where `📁 [[...params]]` is a array of values sent by the route or nothing (`/route-name`).

###### ✅ App Router

```
├── 📁 app
    ├── 📄 layout.js
    ├── 📁 route-name
        ├── 📁 [[...params]]
            ├── 📄 page.js
```

###### ✅ Expo Router

<!-- TODO: Try navigate to '/route-name'  -->

In Expo Router Multiple Parameters are optional by default.

```
├── 📁 app
    ├── 📁 route-name
        ├── 📄 [...params].js
```

```
├── 📁 app
    ├── 📁 route-name
        ├── 📁 [...params]
            ├── 📄 index.js
```

##### Route Groups

Matches route `/route-name`.

###### ✅ App Router

```
├── 📁 app
    ├── 📄 layout.js
    ├── 📁 (group-name)
        ├── 📁 route-name
            ├── 📄 page.js
```

###### ✅ Expo Router

```
├── 📁 app
    ├── 📁 (group-name)
        ├── 📄 route-name.js
```

```
├── 📁 app
    ├── 📁 (group-name)
        ├── 📁 route-name
            ├── 📄 index.js
```

##### Parallel Routes

###### ❌ Expo Router

###### ✅ App Router

Matches route `/`. The `📄 page.js` component of the `📁 @parallel-route-one` and `📁 @parallel-route-two` routes are passed to `📄 layout.js` via `props`.

```
├── 📁 app
    ├── 📄 layout.js
    ├── 📄 page.js
    ├── 📁 @parallel-route-one
        ├── 📄 page.js
    ├── 📁 @parallel-route-two
        ├── 📄 page.js
```

##### Intercepting Routes

###### ❌ Expo Router

###### ✅ App Router

When navigating to `/intercepting-route-name/paramValue` within `/route-name` this route will be intercepted and the URL updated to `/intercepting-route-name/paramValue`, however when this URL is shared the level context defined by convention will be maintained. It can be combined with Parallel Routes to obtain an excellent pattern for modals.

- Convention:
  - `(.)` matchs segments on the same level
  - `(..)` matchs segments one level above
  - `(..)(..)` matchs segments two levels above
  - `(...)` matchs segments from the root app directory

```
├── 📁 app
    ├── 📁 route-name
        ├── 📁 (..)intercepting-route-name
            ├── 📁 [param]
                ├── 📄 page.js
    ├── 📁 intercepting-route-name
        ├── 📁 [param]
            ├── 📄 page.js
```

##### Shared Routes

###### ❌ App Router

###### ✅ Expo Router

Allows the same URL to be rendered with different layouts through the use of Route Groups. All Route Groups have access to `📄 [param].js`: `/(group-name-one)/[param].js`, `/(group-name-two)/[param].js` and `/(group-name-three)/[param].js`.

```
├── 📁 app
    ├── 📁 (group-name-one)
        ├── 📄 _layout.js
        ├── 📄 [param].js
    ├── 📁 (group-name-two)
        ├── 📄 _layout.js
        ├── 📄 [param].js
    ├── 📁 (group-name-three)
        ├── 📄 _layout.js
        ├── 📄 [param].js
```

Duplication can be reduced using Array Syntax:

```
├── 📁 app
    ├── 📁 (group-name-one, group-name-two, group-name-three)
        ├── 📄 _layout.js
        ├── 📄 [param].js
```

### ⛖ Linking and Navigating

#### Navigation with `<Link>` Component

##### Usage

###### Static Route with `href` as `String`

```tsx
import { Link } from "react-universal-layer/navigation";

export default function Page() {
  // Route -> /about
  return <Link href="/about">About</Link>;
}
```

###### Dynamic Route with `href` as `String`

```tsx
import { Link } from "react-universal-layer/navigation";

export default function Page() {
  // Route -> /user/[username]
  return <Link href="/user/gloredo">View user</Link>;
}
```

###### Static Route with `href` as `Object`

```tsx
import { Link } from "react-universal-layer/navigation";

export default function Page() {
  // Route -> /about
  return (
    <Link
      href={{
        pathname: "/about",
      }}
    >
      About
    </Link>
  );
}
```

###### Dynamic Route with `href` as `Object`

```tsx
import { Link } from "react-universal-layer/navigation";

export default function Page() {
  // Route -> /user/[username]
  return (
    <Link
      href={{
        pathname: "/user/[username]",
        params: { username: "gloredo" },
      }}
    >
      View user
    </Link>
  );
}
```

###### Children as a Custom Component

```tsx
import { Pressable, Text } from "react-native";
import { Link } from "react-universal-layer/navigation";

export default function Page() {
  // Route -> /about
  return (
    <Link href="/about">
      <Pressable>
        <Text>About</Text>
      </Pressable>
    </Link>
  );
}
```

##### API Reference

| Param | Type | Required | Default | App Router | Expo Router |
| --- | --- | --- | --- | --- | --- |
| `href` | `String` or `Object` | Yes |  | ✅ | ✅ |
| `replace` | `Boolean` | No | `false` | ✅ | ✅ |
| `prefetch` | `Boolean` | No | `true` | ✅ | ❌ |

<details>

<summary>Implementation Reference</summary>

##### Invoking on App Router

```tsx
import Link from 'next/link';
...
return <Link href={...}>...</Link>;
...
```

##### Invoking on Expo Router

```tsx
import { Pressable, Text } from 'react-native';
import { Link } from 'expo-router';
...
// If the child is a custom component.
// The child component must support the onPress and onClick props, href and accessibilityRole will also be passed down.
return (
  <View>
    <Link href={...}>...</Link>

    <Link href={...} asChild>
      <Pressable>
        <Text>...</Text>
      </Pressable>
    </Link>
  </View>
);
...
```

##### API Reference Comparasion

| Param | Type | Required | App Router | Expo Router | Incompatibility note |
| --- | --- | --- | --- | --- | --- |
| `href` | `String` or `Object` | Yes | ✅ | ✅ | Objects are different. App Router uses `object.query` and Expo Router uses `object.params`. |
| `replace` | `Boolean` | No | ✅ | ✅ |  |
| `prefetch` | `Boolean` | No | ✅ | ❌ |  |
| `asChild` | `Boolean` | No | ❌ | ✅ |  |

##### Integration Rules Implemented

- If `typeof children === React.ReactNode`:
  - Expo Router:
    - Set `asChild={true}`

</details>

#### Imperative Navigation with `router`

<details>

<summary>Implementation Reference</summary>

##### Invoking on App Router

```tsx
import { useRouter } from 'next/router';
...
const router = useRouter();
router.methodName();
...
```

##### Invoking on Expo Router

```tsx
import { router } from 'expo-router';
...
router.methodName();
...
```

##### API Reference Comparasion

| Method | Type | App Router | Expo Router | Incompatibility note |
| --- | --- | --- | --- | --- |
| `push` | App Router: `(url: UrlObject \| String, as: UrlObject \| String, options) => void`. <br> Expo Router: `(href: Href) => void`. | ✅ | ✅ | Types are different. |
| `replace` | App Router: `(url: UrlObject \| String, as: UrlObject \| String, options) => void`. <br> Expo Router: `(href: Href) => void`. | ✅ | ✅ | Types are different. |
| `back` | `() => void` | ✅ | ✅ |  |
| `prefetch` | `(url: UrlObject \| String, as: UrlObject \| String, options) => void` | ✅ | ❌ |  |
| `beforePopState` | `(cb: {url: UrlObject \| String, as: UrlObject \| String, options}) => bool` | ✅ | ❌ |  |
| `reload` | `() => void` | ✅ | ❌ |  |
| `events` | [See in the docs](https://nextjs.org/docs/pages/api-reference/functions/use-router#routerevents) | ✅ | ❌ |  |
| `setParams` | `(params: Record<string, string>) => void` | ❌ | ✅ |  |

</details>

#### Get Param(s) Sent Throug Route

<details>

<summary>Implementation Reference</summary>

##### Invoking on App Router

```tsx
import Link from 'next/link'
...
return <Link
  href={{
    pathname: '/route-name/[paramOne]/[paramTwo]',
    query: { paramOne: 'paramOneValue', paramTwo: 'paramTwoValue' },
  }}
>...</Link>;
...
import { useParams } from 'next/navigation'
...
//URL -> /route-name/paramOneValue/paramTwoValue
const { paramOne, paramTwo } = useParams(); //-> { paramOne: 'paramOneValue', paramTwo: 'paramTwoValue' }
...
```

```tsx
import Link from 'next/link'
...
return <Link
 href='/route-name?searchParam=searchParamValueOne&searchParam=searchParamValueTwo'
>...</Link>;

// OR

return <Link
  href={{
    pathname: '/route-name',
    query: { searchParam: ['searchParamValueOne', 'searchParamValueTwo'] },
  }}
>...</Link>;
...
'use client'

import { useSearchParams } from 'next/navigation'
...
const searchParams = useSearchParams();

//URL -> /route-name?searchParam=searchParamValueOne&searchParam=searchParamValueTwo
const searchParamSingleValue = searchParams.get('searchParam') //-> 'searchParamValueOne'
const searchParamAllValues = searchParams.getAll('searchParam') //-> ['searchParamValueOne', 'searchParamValueTwo']
...
```

##### Invoking on Expo Router

```tsx
import { Link } from 'expo-router';
...
return <Link
 href={{
   pathname: 'route-name',
   params: { paramOne: 'paramOneValue', paramTwo: 'paramTwoValue' }
 }}
>...</Link>;

// OR

return <Link
 href='route-name?paramOne=paramOneValue&paramTwo=paramTwoValue'
>...</Link>;
...
import { useLocalSearchParams, useGlobalSearchParams } from 'expo-router';
...
//Prevent the background screens re-render when params are changed
const { paramOne, paramTwo } = useLocalSearchParams(); //-> { paramOne: 'paramOneValue', paramTwo: 'paramTwoValue' }

//Made the background screens re-render when params are changed
const { paramOne, paramTwo } = useGlobalSearchParams(); //-> { paramOne: 'paramOneValue', paramTwo: 'paramTwoValue' }
...
```

##### Distinction Between Path Parameters and Query Parameters

While the App Router distinguishes the parameters between [Path Parameters](https://swagger.io/docs/specification/describing-parameters/#path-parameters) and [Query Parameters/Query String](https://swagger.io/docs/specification/describing-parameters/#query-parameters) allowing access to them through the `useParams` and `useSearchParams` hooks, Expo Router does not distinguish, bringing both parameters through the `useLocalSearchParams` and `useGlobalSearchParams` hooks.

A limitation of Expo Router is that it only accepts one type of parameter per navigation call on static routes, which means that if you pass the `href.pathname` with Query Parameters and `href.params` with values, only the `href.pathname` values are accessible and `href.params` values are ignored. Let's see an example:

```tsx
import { Link } from 'expo-router';
...
return <Link
 href={{
   pathname: 'route-name?queryParam=queryParamValue',
   params: { pathParam: 'pathParamValue' }
 }}
>...</Link>;
...
import { useLocalSearchParams } from 'expo-router';
...
// Throw an error because pathParam doesn't exist
const { queryParam, pathParam } = useLocalSearchParams();
...
```

However, when using Dynamic Routes it works as expected. Let's see an example:

```tsx
import { Link } from 'expo-router';
...
<Link
 href={{
   pathname: 'route-name/[pathParam]?queryParam=queryParamValue',
   params: { pathParam: 'pathParamValue' }
 }}
>...</Link>
...
import { useLocalSearchParams } from 'expo-router';
...
// Return both values as expected
const { queryParam, pathParam } = useLocalSearchParams(); //-> { queryParam: 'queryParamValue', pathParam: 'pathParamValue' }
...
```

</details>

### 🖼️ `<Image />` Component

### 🔑 Authentication

## 👏 Contributing

If you like React Universal Layer and want to help make it better, just open an issue or discussion in this repository.

## ⚖️ License

The React Universal Layer source code is made available under the [MIT license](LICENSE).
