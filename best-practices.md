# Best Practices

- always remove your `console.log` calls before submitting code
- listen to ESLint warnings
- avoid using `useEffect` as a first resort, effects should be used if there is no other way to achieve your components intended functionality
- use types everywhere you can, avoid implicit `any`'s wherever possible and provide templated functions: `<T>` with types whenever you can
- it is preferred to use `type` to declare your types rather than `interface`, interface is typically only used if you need to `extend` from it later
- most types do not need to be explicitly typed, most types can be safely inferred from your code; however be aware of what may be an `any` and avoid using it in your code
- always wrap your `Promise`'s / async functions in a try/catch block or with a `.catch()` chained function
- if you have a lot of `useState` hook calls in a single component consider converting it to a `useReducer` hook
- avoid using React Context as a first resort, there is nothing inherently wrong with passing many props to a component; if prop drilling does become and issue then context may be used
- attempt to keep your components and functions `PURE`: if given the same arguments your function / component should return the same value / render the same UI
