---
title: 'Mistakes Done While Using Usestate Hook'
date: 2022-10-19T16:56:43+05:30
draft: false
tags:
  - react
---

# Mistakes while using non primitve state

## Same reference problem

When state is of non primitive type then comparison is done based on reference. So even if value is changed but reference is same then it won't execute the render the component again. To avoid this create copy of the state the pass it to setter of state.

**To avoid this**

- In case of object, you can create copy by using spread operator for unchanged part of state and then putting changed part to be merged with it.
- In case of array, you can spread elements using spread operator or use slice function to create copy.

## Different reference but same values

When values of object is same but reference is changed even then it will execute callback again.
