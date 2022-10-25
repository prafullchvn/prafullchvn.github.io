---
title: 'Testing in React Native Project'
date: 2022-10-21T08:33:45+05:30
draft: false
tags:
  - react-native
---

# Setup

```sh
npm install --save-dev @testing-library/react-native --legacy-peer-deps
```

# Jest function

Syntax -

```js
expecte(actual).______; // where _____ you can put building method to assert further
```

## Jest Api functions

### General functions

```js
expect(value).toEqual(someOtherValue);
expect(value).toStrictEqual(someOtherValue);
expect(value).toMatch(/someRegex/);
expect(someObject).toMatchObject(subsetOfObject);

expect(value).toBeTruth();
expect(value).toBeFalsy();

expect(value).toBeDefined();
expect(value).toBeUndefined();

expect(value).toBeNull();
expect(value).toBeNaN();
```

### Based on assertion made

```js
expect.assertions(3); // ensures that 3 assertion have been made in test
expect.hasAssertions(); // ensures that test have at least one assertion
```

### Asserting the array

You can check whether array have particular value or not.

```js
expect([1, 2, 3]).toEqual(expect.arrayContaining([2, 3]));

// Using `.not` you can check assert on negative
expect([1, 2, 3]).not.toEqual(expect.arrayContaining([2, 3]));

expect([1, 2, 3]).toContain(2);

// to check whether array have non literal value
expect(someObject).toContainEqual({ key: value });

expect(someArray).toHaveLength(3);

//
```

### Testing the promise

You can test the promise based on what value it get resolved.
To make Jest wait for async function to be executed, either return the function or use async/await

Syntax

```js
expect(Promise.resolve(2)).resolves.toBe(3); // in case it get resolves
expect(Promise.reject(2)).rejects.toBe(3); // in case it gets rejected
```

### Asserting based interaction with mocked function

#### Based on arguments

```js
const mockedFn = jest.fn();

mockedFn.toHaveBeenCalled(); // ensures that function was called at least once
mockedFn.toHaveBeenCalledTimes(times); // ensures that function was called given number of time
mockedFn.toHaveBeenCalledWith(arg1,...); // ensures that function was called with given argument
mockedFn.toHaveBeenLastCalledWith(arg1,...) // ensures that function was called with given argument last time time
mockedFn.toHaveBeenNthCalledWith(nth,arg1,...) // ensures that function was called with given argument given nth time
```

#### Based on return value

```js
const mockedFn = jest.fn();

mockedFn.toHaveReturned(); // ensures that function returned something
mockedFn.toHaveReturnedTimes(times); // ensures that function was called given number of times
mockedFn.toHaveReturnedWith(returnValue); // ensures that function returned given value
mockedFn.toHaveLastReturnedWith(returnValue); // ensures that function returned given value last time it was called
mockedFn.toHaveNthReturnedWith(nth, returnValue); // ensures that function returned given value nth time it was called
```

### For floating point value

```js
expect(1.23).toBeCloseTo(1.2, 1); //ensures that floating point number is equal to given number to given decimal point
expect(1.23).toEqual(expect.closeTo(1.2, 1));
```

## Jest mocking function

```js
const mocked = jest.fn(); // this will create mock function
```

### Make mock function return some value

```js
const mocked = jest.fn(() => value); // it will return value
// OR
const mocked = jest.fn().mockImplementation(() => value);
```

### Make mock function return some value

```js
const mocked = jest.fn().mockReturnValue(2); // It will always return 2
```

### Make mock fuction return different value when executed first few times

```js
const mocked = jest
                .fn()
                .mockReturnValueOnce(3); // It will return 3 first time it is called
                .mockReturnValueOnce(4); // It will return 4 second time it is called
                .mockReturnValue(5); // It will always return 5

```

### Make mock return some promise

```js
const mocked = jest.fn().mockResolvedValue(2); // It will always return promise which will be resolved with value 2
const mocked = jest.fn().mockResolvedValueOnce(2); // It will only once return promise which will be resolved with value 2
```

## Watch mode

To run the jest in watch mode, you can use -

```sh
jest --watch # to watch for changes and run the test in that file
jest --watchAll # to run all the test regardless of which file is changed
```

# Snapshot Testing

Instead of rendering the DOM tree to get graphical UI, you can render the the component to get some serializable value to compare. It will generate serialized value which will be used to testing the component.

First time the tests are run it creates the snapshot file. Afterwards it uses the same file to compare and run the tests.

_Snapshot files are artifact and should be committed along side code and should be reviewed along side the code_

When the snapshot tests fails it means two things -

1.  There is some bug and component is rendered wrongly.
2.  There are some intentional changes in component.

Example

Let's take Card component.

```js
import React from 'react';
import { Text, View } from 'react-native';

export type cardProps = {
  name: string,
  address: string,
};

const Card = ({ name, address }: cardProps) => {
  return (
    <View>
      <Text>{name}</Text>
      <Text>{address} </Text>
    </View>
  );
};

export default Card;
```

Generated snapshot is like this

```snap
// Jest Snapshot v1, https://goo.gl/fbAQLP

exports[`Should render the card component 1`] = `
<View>
  <Text>
    John
  </Text>
  <Text>
    Nashik

  </Text>
</View>
`;
```

## Changing the snapshot in case of intentional changes

In this case, to update the snapshot to match snapshot with latest changes use following command.

```sh
jest -updateSnapshot
```

**You can update the failes snapshot in watch mode also.**

## Inline snapshot

It's same as the snapshot test, except the part that snapshot is generated back in source code.

_In order to use the inline snapshot you need to have the prettier installed in on your machine_

Example

```js
it('Should generate the inline snapshot', () => {
  const card = renderer.create(<Card name='John' address='Nashik' />).toJSON();

  expect(card).toMatchInlineSnapshot(`
    <View>
      <Text>
        John
      </Text>
      <Text>
        Nashik
         
      </Text>
    </View>
  `);
});
```

# Mocking

As specified above in Jest function you can use those to mock the function.

## Mocking module

Suppose you are fetching data from the some API using `axios`. But in testing you don't want to hit the actual API to test. So here you can mock the `axios` module along with the method that you are using in testing.

```js
import 'react-native';
import React from 'react';
import axios from 'axios';

import getUser from '../src/card';

jest.mock('axios');

it('should render the card', () => {
  const data = { name: 'abc', age: 21 };
  axios.get.mockResolvedValue(data);

  return getUser().then((val) =>
    expect(val).toEqual('Name of user is abc of age 21')
  );
});
```

## Mocking Partial. - Mocking only subset of module

In some cases you want to mock only some function of module and keep rest of the exports same. In that case you can mock only part by passing second parameter to mock function.

```js
import axios,{get,...restOfImports} from 'axios';

jest.mock('axios', () => {
  return {
    __esModule: true, // to allow the default import in non js module
    get:()=>{return new Promise.resolve({someKey:someValue})},
    ...restOfImports
  };
});
```

Here we have only mocked the axios module keeping rest of exports from module same. If you are wondering why `__esModule` flag I have given reference link below check it out.

## What is use of method mockImplementation if jest.fn(defaultImplemention) is there?

This method is useful when you have imported from some other module but need to be mocked again.

## Giving mock a name

Why is it better to have name for mock function? It proves useful when you have some error thrown on your screen. When error is printed on screen it doesn't print jest.fn() instead prints the name of function that you have given.

```js
const mockedFn = mock.fn().mockName('some name');
```

## Checking usage of mock

Mock have following properties we can use to check data that is used with mock function.

1.  `mockFn.mock.calls` - it return the array of arguments(in form of array).
2.  `mockFn.mock.results` - it return the array of return values.
3.  `mockFn.mock.instances` - it return the array of instances initialized from this mockFn.

# Further read

- [When to use snapshot testing](https://benmccormick.org/2016/09/19/testing-with-jest-snapshots-first-impressions/)

- [Mocking](https://jestjs.io/docs/26.x/mock-functions)

# Reference

- [Egghead video on snapshot testing](https://egghead.io/lessons/javascript-use-jest-s-snapshot-testing-feature?pl=testing-javascript-with-jest-a36c4074)

- [\_\_esModule flag](https://stackoverflow.com/questions/50943704/whats-the-purpose-of-object-definepropertyexports-esmodule-value-0)
