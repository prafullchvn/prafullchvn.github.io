---
title: 'Useeffect Hook in React'
date: 2022-10-19T16:31:43+05:30
draft: false
tags:
  - react-native
---

useEffect hook in react native is one of the very useful and most used hook, (at least for me it is ;) ). There are various versions of useEffect hook that I am going to talk about in this blog.

# Without dependency

Following version of useEffect runs the callback each time the component that it is used in is rendered.

Syntax -

```js
useEffect(() => {
  /**
   * some code here
   */
});
```

# With dependency

Following version of useEffect is executed each time depedency is changes. Dependency are passed as second argument to useEffect hook in form of array.

```js
useEffect(() => {
  /**
   * some code here
   *
   */
}, [...dependencies]);
```

# As componentDidMount method

Following version of useEffect is used as componentDidMount method used in class component, which means it executes the callback when component is mounted first time. Generally code for API calls or fetching data from some data source comes here.

```js
useEffect(() => {
  /**
   * some code here
   *
   */
}, []);
```

# Cleanup function

All the logic that we put in callback given to useEffect are known as Side Effect in react world. To perform these sideEffect we utilize some resource which we need to clear after component is unmounted. Following version of useEffect is used to clear the resources which are used in useEffect's callback.

**This version of useEffect can be combined with above three version that about**

```js
useEffect(() => {
  /**
   * some code here
   *
   */
  return () => {
    // clean up code goes here
  };
});
```

# Types of dependency

There are two types of dependency in useEffect.

1.  Primitive dependency
2.  Non primitive dependency

## Primitive dependency

Dependencies which are of primitive type are known as primitive dependency.

E.g. `1(number), "some string"(string), true(boolean)`

## Non primitive dependency

Dependencies which are of non primitive type like object, array are known as non primitive depedency.

E.g. `{key:value}(object), [val1, val2](array)`

### Mistakes while using non primitve dependency

Callback of useEffect is executed when dependency changes. When depedency is of non primitive type then comparison is done based on reference. So even if value is changed but reference is same then it won't execute the callback. This is same for useState hook when state is of non primitive type.

When values of object is same but reference is changed even then it will execute callback again.
To avoid this you can use `useMemo` hook or specify each the dependency separately.
