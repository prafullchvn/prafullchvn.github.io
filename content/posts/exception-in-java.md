---
title: 'Exception in Java'
date: 2022-09-13T09:03:42+05:30
draft: true
---

# Catch or Specify Requirement

# Types of Exeception

## Checked Exception

E.g. Reading file whose path is given by user.
Requires Catch or Specify Requirement.

## Unchecked Exception

Don't requires Catch or Specify Requirement.
Indication of bug present in application.
If application throw this kind of exception then application logic should be changed in such way that it doesn't cause exception.
These are internal to application and application can not anticipate or recover from.

## Error

Don't requires Catch or Specify Requirement.
These are external to application and application can not anticipate or recover from.
Causes can be hardaware problem.

# Reference

[Exception](https://docs.oracle.com/javase/tutorial/essential/exceptions/index.html)
[Chained Exception](https://docs.oracle.com/javase/tutorial/essential/exceptions/chained.html)
![Exception Hierarchy](/images/exceptions-in-java/exception-hierarchy.jpeg)
