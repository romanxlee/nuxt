---
title: 'abortNavigation'
description: 'abortNavigation is a helper function that prevents navigation from taking place and throws an error if one is set as a parameter.'
links:
  - label: Исходники
    icon: i-simple-icons-github
    to: https://github.com/nuxt/nuxt/blob/main/packages/nuxt/src/app/composables/router.ts
    size: xs
---

::warning
`abortNavigation` is only usable inside a [route middleware handler](/docs/guide/directory-structure/middleware).
::

## Тип

```ts
abortNavigation(err?: Error | string): false
```

## Параметры

### `err`

- **тип**: [`Error`](https://developer.mozilla.org/pl/docs/Web/JavaScript/Reference/Global_Objects/Error) | `string`

  Optional error to be thrown by `abortNavigation`.

## Примеры

The example below shows how you can use `abortNavigation` in a route middleware to prevent unauthorized route access:

```ts [middleware/auth.ts]
export default defineNuxtRouteMiddleware((to, from) => {
  const user = useState('user')

  if (!user.value.isAuthorized) {
    return abortNavigation()
  }

  if (to.path !== '/edit-post') {
    return navigateTo('/edit-post')
  }
})
```

### `err` as a String

You can pass the error as a string:

```ts [middleware/auth.ts]
export default defineNuxtRouteMiddleware((to, from) => {
  const user = useState('user')

  if (!user.value.isAuthorized) {
    return abortNavigation('Insufficient permissions.')
  }
})
```

### `err` as an Error Object

You can pass the error as an [`Error`](https://developer.mozilla.org/pl/docs/Web/JavaScript/Reference/Global_Objects/Error) object, e.g. caught by the `catch`-block:

```ts [middleware/auth.ts]
export default defineNuxtRouteMiddleware((to, from) => {
  try {
    /* code that might throw an error */
  } catch (err) {
    return abortNavigation(err)
  }
})
```
