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

- [🚀 Goal and Guidelines](#-goal-and-guidelines)
- [🗺 Project Layout](#-project-layout)
- [📚 Documentation](#-documentation)
- [Navigation](#navigation)
  - [Roles of Folders and Files](#roles-of-folders-and-files)
    - [Root Route](#root-route)
      - [App Router](#app-router)
      - [Expo Router](#expo-router)
    - [Named Routes](#named-routes)
      - [App Router](#app-router-1)
      - [Expo Router](#expo-router-1)
    - [Nested Routes](#nested-routes)
      - [App Router](#app-router-2)
      - [Expo Router](#expo-router-2)
    - [Dynamic Routes with One Parameter](#dynamic-routes-with-one-parameter)
      - [App Router](#app-router-3)
      - [Expo Router](#expo-router-3)
    - [Dynamic Routes with Multiple Parameters](#dynamic-routes-with-multiple-parameters)
      - [App Router](#app-router-4)
      - [Expo Router](#expo-router-4)
    - [Route Groups](#route-groups)
      - [App Router](#app-router-5)
      - [Expo Router](#expo-router-5)
    - [Parallel Routes](#parallel-routes)
      - [App Router](#app-router-6)
      - [Expo Router](#expo-router-6)
  - [Linking and Navigating](#linking-and-navigating)
    - [Navigation with `<Link>` component](#navigation-with-link-component)
      - [Usage](#usage)
        - [Basic usage](#basic-usage)
        - [Usage with a custom component](#usage-with-a-custom-component)
      - [API Reference](#api-reference)
      - [Invoking on App Router](#invoking-on-app-router)
      - [Invoking on Expo Router](#invoking-on-expo-router)
      - [API Reference Comparasion](#api-reference-comparasion)
      - [Integration Rules Implemented](#integration-rules-implemented)
    - [Imperative Navigation with `router`](#imperative-navigation-with-router)
      - [Invoking on App Router](#invoking-on-app-router-1)
      - [Invoking on Expo Router](#invoking-on-expo-router-1)
      - [API Reference Comparasion](#api-reference-comparasion-1)
    - [Get Param(s) Sent Throug Route](#get-params-sent-throug-route)
      - [Invoking on App Router](#invoking-on-app-router-2)
      - [Invoking on Expo Router](#invoking-on-expo-router-2)
      - [Distinction Between Path Parameters and Query Parameters](#distinction-between-path-parameters-and-query-parameters)
- [👏 Contributing](#-contributing)
- [⚖️ License](#️-license)

## 🚀 Goal and Guidelines

## 🗺 Project Layout

## 📚 Documentation

## Navigation

### Roles of Folders and Files

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

#### Navigation with `<Link>` component

##### Usage

###### Basic usage

> If `props.children` is of type `String`.

```ts
import { Link } from "react-universal-layer/navigation";

export default function Page() {
  return (
    <View>
      // Static route with href as String
      // Route -> /about
      <Link href="/about">About</Link>

      // Dynamic route with href as String
      // Route -> /user/[username]
      <Link href="/user/gloredo">View user</Link>
    </View>
  );
}
```

###### Usage with a custom component

> If `props.children` is of type `React.ReactNode`.

```ts
import React from "react";
import { Pressable, Text } from "react-native";
import { Link } from "react-universal-layer/navigation";

// ref need to be passed to the element for proper handling in App Router
const MyButton = React.forwardRef((props, ref) => {
  return (
    <Pressable {...props} ref={ref}>
      <Text>...</Text>
    </Pressable>
  );
});

export default function Page() {
  // Route -> /about
  return (
    <Link href="/about">
      <MyButton />
    </Link>
  );
}
```

##### API Reference

| Param      | Type                 | Required | App Router | Expo Router |
| ---------- | -------------------- | -------- | ---------- | ----------- |
| `href`     | `String` or `Object` | Yes      | ✅         | ✅          |
| `replace`  | `Boolean`            | No       | ✅         | ✅          |
| `prefetch` | `Boolean`            | No       | ✅         | ❌          |

<details>

<summary>Implementation Reference</summary>

##### Invoking on App Router

```ts
import Link from 'next/link';
import styled from 'styled-components'
...
// onClick, href, and ref need to be passed to the DOM element for proper handling
const MyButton = React.forwardRef(({ onClick, href }, ref) => {
  return (
    <a href={href} onClick={onClick} ref={ref}>...</a>
  )
})
...
// This creates a custom component that wraps an <a> tag
const RedLink = styled.a`
  color: red;
`

return (
  <View>
    <Link href={...}>...</Link>

    // If the child is a custom component that wraps an <a> tag
    <Link href={...} passHref legacyBehavior>
      <RedLink>...</RedLink>
    </Link>

    // If the child is a functional component
    <Link href={...} passHref legacyBehavior>
      <MyButton />
    </Link>
  </View>
);
...
```

##### Invoking on Expo Router

```ts
import { Pressable, Text } from "react-native";
import { Link } from 'expo-router';
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
| `passHref` | `Boolean` | No | ✅ | ❌ |  |
| `scroll` | `Boolean` | No | ✅ | ❌ |  |
| `shallow` | `Boolean` | No | ✅ | ❌ |  |
| `locale` | `Boolean` | No | ✅ | ❌ |  |
| `asChild` | `Boolean` | No | ❌ | ✅ |  |

##### Integration Rules Implemented

- If `typeof children === React.ReactNode`:
  - App Router
    - Set `passHref={true}`
    - Set `legacyBehavior={true}`
  - Expo Router
    - Set `asChild={true}`

</details>

#### Imperative Navigation with `router`

<details>

<summary>Implementation Reference</summary>

##### Invoking on App Router

```ts
import { useRouter } from 'next/router';
...
const router = useRouter();
router.methodName();
...
```

##### Invoking on Expo Router

```ts
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

```ts
import { useParams } from 'next/navigation'
...
//Route -> /route-name/[paramOne]/[paramTwo]
const { paramOne, paramTwo } = useParams();
...
```

```ts
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

```ts
import { useLocalSearchParams, useGlobalSearchParams } from 'expo-router';
...
// <Link
//  href={{
//    pathname: 'route-name',
//    params: { paramOne: 'paramOneValue', paramTwo: 'paramTwoValue' }
//  }}
// >...</Link>
//
// OR
//
// <Link
//  href='route-name?paramOne=paramOneValue&paramTwo=paramTwoValue'
// >...</Link>

//Prevent the background screens re-render when params are changed
const { paramOne, paramTwo } = useLocalSearchParams(); //-> {paramOne: 'paramOneValue', paramTwo: 'paramTwoValue'}

//Made the background screens re-render when params are changed
const { paramOne, paramTwo } = useGlobalSearchParams(); //-> {paramOne: 'paramOneValue', paramTwo: 'paramTwoValue'}
...
```

##### Distinction Between Path Parameters and Query Parameters

While the App Router distinguishes the parameters between [Path Parameters](https://swagger.io/docs/specification/describing-parameters/#path-parameters) and [Query Parameters/Query String](https://swagger.io/docs/specification/describing-parameters/#query-parameters) allowing access to them through the `useParams` and `useSearchParams` hooks, Expo Router does not distinguish, bringing both parameters through the `useLocalSearchParams` and `useGlobalSearchParams` hooks.

A limitation of Expo Router is that it only accepts one type of parameter per navigation call, which means that if you pass the `href.pathname` with Query Parameters and `href.params` with values, only the `href.pathname` values are accessible and `href.params` values are ignored. Let's see an example:

```ts
import { useLocalSearchParams } from 'expo-router';
...
// <Link
//  href={{
//    pathname: 'route-name?queryParam=queryParamValue',
//    params: { pathParam: 'pathParamValue' }
//  }}
// >...</Link>

// Throw an error because pathParam doesn't exist
const { queryParam, pathParam } = useLocalSearchParams();
...
```

However, when using Dynamic Routes it works as expected. Let's see an example:

```ts
import { useLocalSearchParams } from 'expo-router';
...
// <Link
//  href={{
//    pathname: 'route-name/[pathParam]?queryParam=queryParamValue',
//    params: { pathParam: 'pathParamValue' }
//  }}
// >...</Link>

// Return both values as expected
const { queryParam, pathParam } = useLocalSearchParams(); //-> {queryParam: 'queryParamValue', pathParam: 'pathParamValue'}
...
```

</details>

## 👏 Contributing

If you like React Universal Layer and want to help make it better, just open an issue or discussion in this repository.

## ⚖️ License

The React Universal Layer source code is made available under the [MIT license](LICENSE).
