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
      - [Invoking on App Router](#invoking-on-app-router)
      - [Invoking on Expo Router](#invoking-on-expo-router)
      - [API reference comparasion](#api-reference-comparasion)
    - [Imperative Navigation with `router`](#imperative-navigation-with-router)
      - [Invoking on App Router](#invoking-on-app-router-1)
      - [Invoking on Expo Router](#invoking-on-expo-router-1)
      - [API reference comparasion](#api-reference-comparasion-1)
    - [Get param(s) sent throug route](#get-params-sent-throug-route)
      - [Invoking on App Router](#invoking-on-app-router-2)
      - [Invoking on Expo Router](#invoking-on-expo-router-2)
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

#### Dynamic Routes with Multiple Parameters

Matches route `/route-name/[...params]` where `[params]` is a array of values sent by the route.

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

<details>

<summary>Implementation reference</summary>

##### Invoking on App Router

```js
import Link from 'next/link';
...
return <Link>...</Link>
...
```

##### Invoking on Expo Router

```js
import { Link } from 'expo-router';
...
return <Link>...</Link>
...
```

##### API reference comparasion

| Param | Type | Required | App Router | Expo Router | Incompatibility note |
| --- | --- | --- | --- | --- | --- |
| `href` | `String` or `Object` | Yes | ✅ | ✅ | Objects are different. Next.js uses `object.query` and Expo uses `object.params`. |
| `replace` | `Boolean` | No | ✅ | ✅ |  |
| `prefetch` | `Boolean` | No | ✅ | ❌ |  |
| `asChild` | `Boolean` | No | ❌ | ✅ |  |

</details>

#### Imperative Navigation with `router`

<details>

<summary>Implementation reference</summary>

##### Invoking on App Router

```js
import { useRouter } from 'next/router';
...
const router = useRouter();
router.methodName();
...
```

##### Invoking on Expo Router

```js
import { router } from 'expo-router';
...
router.methodName();
...
```

##### API reference comparasion

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

#### Get param(s) sent throug route

<details>

<summary>Implementation reference</summary>

##### Invoking on App Router

```js
import { useParams } from 'next/navigation'
...
//Route -> /route-name/[paramOne]/[paramTwo]
const { paramOne, paramTwo } = useParams();
...
```

```js
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

```js
import { useLocalSearchParams, useGlobalSearchParams } from 'expo-router';
...
//Prevent the background screens re-render when params are changed
const { paramOne, paramTwo } = useLocalSearchParams();

//Made the background screens re-render when params are changed
const { paramOne, paramTwo } = useGlobalSearchParams();
...
```

</details>

## 👏 Contributing

If you like React Universal Layer and want to help make it better, just open an issue or discussion in this repository.

## ⚖️ License

The React Universal Layer source code is made available under the [MIT license](LICENSE).
