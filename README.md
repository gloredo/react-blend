# Routing Fundamentals

## Roles of Folders and Files

### Root Route
Matches route  `/`.

App Router
```
├── 📁 app
    ├── 📄 page.js
```

Expo Router
```
├── 📁 app
    ├── 📄 index.js
```

### Named Routes
Matches route  `/route-name`.

App Router
```
├── 📁 app
    ├── 📁 route-name
        ├── 📄 page.js 
```

Expo Router
```
├── 📁 app
    ├── 📄 route-name.js
```

```
├── 📁 app
    ├── 📁 route-name
        ├── 📄 index.js
```

### Nested Routes
Matches route  `/parent-route-name/child-route-name`

App Router
```
├── 📁 app
    ├── 📁 parent-route-name
        ├── 📁 child-route-name
            ├── 📄 page.js
```

Expo Router
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

### Dynamic Routes with One Parameter
Matches route  `/route-name/[param]`  where  `[param]`  is a single value sent by the route.

App Router
```
├── 📁 app
    ├── 📁 route-name
        ├── 📁 [param]
            ├── 📄 page.js
```

Expo Router
```
├── 📁 app
    ├── 📁 route-name
        ├── 📄 [param].js
```

### Dynamic Routes with Multiple Parameters
Matches route  `/route-name/[...params]`  where  `[params]`  is a array of values sent by the route.

App Router
```
├── 📁 app
    ├── 📁 route-name
        ├── 📁 [...params]
            ├── 📄 page.js
```

Expo Router
```
├── 📁 app
    ├── 📁 route-name
        ├── 📄 [...params].js
```

### Route Groups
Matches route  `/route-name` .

App Router
```
├── 📁 app
    ├── 📁 (group-name)
        ├── 📁 route-name
            ├── 📄 page.js
```

Expo Router
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

### Parallel Routes
Matches route  `/`.

App Router
```
├── 📁 app
    ├── 📁 @parallel-route-one
        ├── 📄 page.js
    ├── 📁 @parallel-route-two
        ├── 📄 page.js
    ├── 📄 layout.js
    ├── 📄 page.js
```

Expo Router
Not supported.

### Intercepting Routes

## Linking and Navigating

### `<Link>` Component

| Param | Type | Required | App Router | Expo Router | Incompatibility note |
| - | - | - | - | - | - | 
| `href` | `String` or `Object` | Yes | ✅ | ✅ | Objects are different. Next.js uses `object.query` and Expo uses `object.params`. |
| `replace` | `Boolean` | No | ✅ | ✅ | |
| `prefetch` | `Boolean` | No | ✅ | ❌ | |
| `asChild` | `Boolean` | No | ❌ | ✅ | |

### Imperative navigation with `router`

Invoking on App Router
```js
import { useRouter } from 'next/router'
...
const router = useRouter()
router.methodName()
...
```

Invoking on Expo Router
```js
import { router } from 'expo-router';
...
router.methodName()
...
```

| Method | Type | App Router | Expo Router | Incompatibility note |
| - | - | - | - | - | 
| `push` | App Router: `(url: UrlObject \| String, as: UrlObject \| String, options) => void`. <br> Expo Router: `(href: Href) => void`. | ✅ | ✅ | Types are different. |
| `replace` | App Router: `(url: UrlObject \| String, as: UrlObject \| String, options) => void`. <br> Expo Router: `(href: Href) => void`. | ✅ | ✅ | Types are different. |
| `back` | `() => void` | ✅ | ✅ | |
| `prefetch` | `(url: UrlObject \| String, as: UrlObject \| String, options) => void` | ✅ | ❌ | |
| `beforePopState` | `(cb: {url: UrlObject \| String, as: UrlObject \| String, options}) => bool` | ✅ | ❌ | |
| `reload` | `() => void` | ✅ | ❌ | |
| `events` | [See in the docs](https://nextjs.org/docs/pages/api-reference/functions/use-router#routerevents) | ✅ | ❌ | |
| `setParams` | `(params: Record<string, string>) => void` | ❌ | ✅ | |

