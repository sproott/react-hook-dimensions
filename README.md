# react-hook-dimensions

Get full control over your dimensions!

React Hook to get DOM Element `BoundingClientRect` together with the `page offset` snapshot, that covers all your needs.

What makes the package different - **You can trigger an update when you really need it.**

## Reason

Countless packages do the same thing, but **all** of them trigger dimensions update whenever they want.

Let's take a look:

- **[react-use-dimensions](https://github.com/Swizec/useDimensions)** - Uses `resize` and `scroll` event listeners. It's the most popular one. Seriously?

- **[react-cool-dimensions](https://github.com/wellyshen/react-cool-dimensions)** - Uses `ResizeObserver` under the hood. Not bad, but what if you don't want to change state on every resize, but update multiple elements dimensions simultaneously?

- **[react-dimensions-hook](https://github.com/cubonacci/react-dimensions-hook)** - `ResizeObserver` again. But you also can pass an array of dependencies, although it's not documented... I started with a few PRs to the package but decided to create a separate thing because of many breaking changes.

- **[react-hooks-get-dimensions](https://github.com/ilhantekir/React-hooks-get-dimensions)** - Uses `resize` event listener. That's all.

- **[use-element-dimensions](https://github.com/danielkov/use-element-dimensions)** - Uses `ResizeObserver`. Returns only width and height.

I hope you can see, that none let you control dimensions update by yourself.

## Usage

```javascript
import { useDimensions } from 'react-hook-dimensions';

/* ... */

const [elementRef, elementDimensions, updateElementDimensions] = useDimensions({
  dependencies: [],
  defaults: {
    heigth: 300,
    scrollY: 123,
  },
});
```

1. Pass `ref` that's called `elementRef` here to an element you want to measure.
2. Then take `dimensions data` from the second param. Although initially, all values are going to be zeros.
3. There are two ways to update dimensions:
   3.1. Use `dependencies` options. When one of the dependencies changes, the hook updates dimensions. You can set it to an empty array if you want to have **computed value from start**.
   3.2. Call the `updateElementDimensions` function, that's the third param.

## Details

- If `dependencies` option isn't set, then `dimensions` value will be zero till the `update` function call.
- You can set `defaults` option, that will override initial `dimension` value. It may be usefull for _SSR_.
- The `dimensions` object has `scrollX` and `scrollY` values that computed on `update`, together with `BoundingClientRect`. Due to this you can cumpute element's position on the page (not only screen).
- **100% TypeScript**.

## Use cases

_In progress_
