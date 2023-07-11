<p align="center">
    <h1 align="center">React Universal Layer</h1>
</p>
<p align="center">
  <a aria-label="Join our Discord" href="" target="_blank">
    <img alt="Discord" src="https://img.shields.io/discord/695411232856997968.svg?style=flat-square&labelColor=000000&color=4630EB&logo=discord&logoColor=FFFFFF&label=" />
  </a>
  <a aria-label="React Universal Layer is free to use" href="" target="_blank">
    <img alt="License: MIT" src="https://img.shields.io/badge/License-MIT-success.svg?style=flat-square&color=33CC12" target="_blank" />
  </a>
</p>

---

- [📏 Goal and Guidelines](#-goal-and-guidelines)
  - [Making Cross-Platform Development a Breeze](#making-cross-platform-development-a-breeze)
  - [Staying as Close to the Original Design as Possible](#staying-as-close-to-the-original-design-as-possible)
  - [Be Small to Always Stay Up to Date](#be-small-to-always-stay-up-to-date)
  - [Implementation Reference Sections](#implementation-reference-sections)
- [📚 Documentation](#-documentation)
  - [Roles of Folders and Files](#roles-of-folders-and-files)
    - [Root Route](#root-route)
    - [Named Routes](#named-routes)
    - [Nested Routes](#nested-routes)
    - [Dynamic Routes with One Parameter](#dynamic-routes-with-one-parameter)
    - [Dynamic Routes with Multiple Parameters](#dynamic-routes-with-multiple-parameters)
    - [Route Groups](#route-groups)
    - [Parallel Routes](#parallel-routes)
  - [Linking and Navigating](#linking-and-navigating)
    - [Navigation with `<Link>` Component](#navigation-with-link-component)
    - [Imperative Navigation with `router`](#imperative-navigation-with-router)
    - [Get Param(s) Sent Throug Route](#get-params-sent-throug-route)
- [👏 Contributing](#-contributing)
- [⚖️ License](#️-license)

> **ATTENTION!**
>
> This package **does NOT support Next.js's Pages Router and React Navigation**, it only supports Next.js's App Router and Expo Router. [Read more](#be-small-to-always-stay-up-to-date).

## 📏 Goal and Guidelines

The **React Universal Layer** is a thin layer of integration between the [Next.js](https://nextjs.org/) and [Expo](https://expo.dev/home) APIs, solving API compatibility issues and providing a unified API that works with very little interference between framework APIs. The main pain solved is not having to worry about the specifics of each framework and simply using their available APIs, it's designed in a way that you don't even notice it's there.

### Making Cross-Platform Development a Breeze

Writing code that works on all platforms (Web, Android, iOS, Desktop) is a difficult task, but writing code that works on all platforms using the best of their native environments is an even harder task. This is the main objective of "React Universal Apps", the idea of writing React code that uses the best and most modern development, which currently boils down to Expo ([React Native](https://reactnative.dev/)) for Android and iOS, and Next.js ([React DOM](https://react.dev/)) for Web. Desktop development is a more complex topic as there are two good ways to go: building web-based apps with [Electron](https://www.electronjs.org/) or [Tauri](https://tauri.app/), or building native apps with [React Native Windows](https://github.com/microsoft/react-native-windows) and [React Native macOS](https://github.com/microsoft/react-native-macos).

### Staying as Close to the Original Design as Possible

We never intend to create new features or offer APIs that are not available in both frameworks, limiting ourselves to creating types, parameters or methods if really necessary. The whole integration rule is under the hood so you don't have to learn anything new.

### Be Small to Always Stay Up to Date

This project needs to be always up to date to work properly, so keeping things small and simple is essential to avoid falling into trouble. Unfortunately this meant that things had to be cut back and it was decided to drop support for Next.js's Pages Router and React Navigation, focusing all resources on integrating Next.js's App Router and Expo Router APIs. This situation may change in the future, let us know!

### Implementation Reference Sections

Each section of the documentation can have a hidden section at the end called "Implementation Reference", responsible for gathering all the information necessary to demonstrate the use and differences between the frameworks, as well as mapping possible new additions that need to be made for full integration. You don't have to worry about it, it's just for curious people and developers of this package.

## 📚 Documentation

### Roles of Folders and Files

There is nothing new here, this section of the documentation has the sole purpose of summarizing and keeping track of all folder and file scenarios possible to implement in each framework.

#### Root Route

Matches route `/`.

##### App Router

```
├── 📁 app
    ├── 📄 page.js
```

##### Expo Router

```
├── 📁 app
    ├── 📄 index.js
```

#### Named Routes

Matches route `/route-name`.

##### App Router

```
├── 📁 app
    ├── 📁 route-name
        ├── 📄 page.js
```

##### Expo Router

```
├── 📁 app
    ├── 📄 route-name.js
```

```
├── 📁 app
    ├── 📁 route-name
        ├── 📄 index.js
```

#### Nested Routes

Matches route `/parent-route-name/child-route-name`.

##### App Router

```
├── 📁 app
    ├── 📁 parent-route-name
        ├── 📁 child-route-name
            ├── 📄 page.js
```

##### Expo Router

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

#### Dynamic Routes with One Parameter

Matches route `/route-name/[param]` where `[param]` is a single value sent by the route.

##### App Router

```
├── 📁 app
    ├── 📁 route-name
        ├── 📁 [param]
            ├── 📄 page.js
```

##### Expo Router

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

#### Dynamic Routes with Multiple Parameters

Matches route `/route-name/[...params]` where `[...params]` is a array of values sent by the route.

##### App Router

```
├── 📁 app
    ├── 📁 route-name
        ├── 📁 [...params]
            ├── 📄 page.js
```

##### Expo Router

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

#### Route Groups

Matches route `/route-name`.

##### App Router

```
├── 📁 app
    ├── 📁 (group-name)
        ├── 📁 route-name
            ├── 📄 page.js
```

##### Expo Router

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

#### Parallel Routes

Matches route `/`.

##### App Router

```
├── 📁 app
    ├── 📁 @parallel-route-one
        ├── 📄 page.js
    ├── 📁 @parallel-route-two
        ├── 📄 page.js
    ├── 📄 layout.js
    ├── 📄 page.js
```

##### Expo Router

Not supported.

### Linking and Navigating

#### Navigation with `<Link>` Component

##### Usage

###### Static Route with `href` as `String`

```ts
import { Link } from "react-universal-layer/navigation";

export default function Page() {
  // Route -> /about
  return <Link href="/about">About</Link>;
}
```

###### Dynamic Route with `href` as `String`

```ts
import { Link } from "react-universal-layer/navigation";

export default function Page() {
  // Route -> /user/[username]
  return <Link href="/user/gloredo">View user</Link>;
}
```

###### Static Route with `href` as `Object`

```ts
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

```ts
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

```ts
import { Pressable, Text } from "react-native";
import { Link } from "react-universal-layer/navigation";

export default function Page() {
  return (
    // Route -> /about
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

```ts
import Link from "next/link";
...
return <Link href={...}>...</Link>;
...
```

##### Invoking on Expo Router

```ts
import { Pressable, Text } from "react-native";
import { Link } from "expo-router";
...
return (
  <View>
    <Link href={...}>...</Link>

    // If the child is a custom component
    <Link href={...} asChild>
      // The child component must support the onPress and onClick props, href and accessibilityRole will also be passed down
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

```ts
import { useRouter } from "next/router";
...
const router = useRouter();
router.methodName();
...
```

##### Invoking on Expo Router

```ts
import { router } from "expo-router";
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

```ts
import { useParams } from "next/navigation"
...
//Route -> /route-name/[paramOne]/[paramTwo]
const { paramOne, paramTwo } = useParams();
...
```

```ts
"use client"

import { useSearchParams } from "next/navigation"
...
const searchParams = useSearchParams();

//URL -> /route-name?searchParam=searchParamValueOne&searchParam=searchParamValueTwo
const searchParamSingleValue = searchParams.get("searchParam") //-> "searchParamValueOne"
const searchParamAllValues = searchParams.getAll("searchParam") //-> ["searchParamValueOne", "searchParamValueTwo"]
...
```

##### Invoking on Expo Router

```ts
import { useLocalSearchParams, useGlobalSearchParams } from "expo-router";
...
// <Link
//  href={{
//    pathname: "route-name",
//    params: { paramOne: "paramOneValue", paramTwo: "paramTwoValue" }
//  }}
// >...</Link>
//
// OR
//
// <Link
//  href="route-name?paramOne=paramOneValue&paramTwo=paramTwoValue"
// >...</Link>

//Prevent the background screens re-render when params are changed
const { paramOne, paramTwo } = useLocalSearchParams(); //-> {paramOne: "paramOneValue", paramTwo: "paramTwoValue"}

//Made the background screens re-render when params are changed
const { paramOne, paramTwo } = useGlobalSearchParams(); //-> {paramOne: "paramOneValue", paramTwo: "paramTwoValue"}
...
```

##### Distinction Between Path Parameters and Query Parameters

While the App Router distinguishes the parameters between [Path Parameters](https://swagger.io/docs/specification/describing-parameters/#path-parameters) and [Query Parameters/Query String](https://swagger.io/docs/specification/describing-parameters/#query-parameters) allowing access to them through the `useParams` and `useSearchParams` hooks, Expo Router does not distinguish, bringing both parameters through the `useLocalSearchParams` and `useGlobalSearchParams` hooks.

A limitation of Expo Router is that it only accepts one type of parameter per navigation call, which means that if you pass the `href.pathname` with Query Parameters and `href.params` with values, only the `href.pathname` values are accessible and `href.params` values are ignored. Let"s see an example:

```ts
import { useLocalSearchParams } from "expo-router";
...
// <Link
//  href={{
//    pathname: "route-name?queryParam=queryParamValue",
//    params: { pathParam: "pathParamValue" }
//  }}
// >...</Link>

// Throw an error because pathParam doesn"t exist
const { queryParam, pathParam } = useLocalSearchParams();
...
```

However, when using Dynamic Routes it works as expected. Let"s see an example:

```ts
import { useLocalSearchParams } from "expo-router";
...
// <Link
//  href={{
//    pathname: "route-name/[pathParam]?queryParam=queryParamValue",
//    params: { pathParam: "pathParamValue" }
//  }}
// >...</Link>

// Return both values as expected
const { queryParam, pathParam } = useLocalSearchParams(); //-> {queryParam: "queryParamValue", pathParam: "pathParamValue"}
...
```

</details>

## 👏 Contributing

If you like React Universal Layer and want to help make it better, just open an issue or discussion in this repository.

## ⚖️ License

The React Universal Layer source code is made available under the [MIT license](LICENSE).
