---
title: 'Packages in Java'
date: 2022-09-03T11:27:21+05:30
draft: false
tags:
  - java
---

# Package

Package is group of related types.

Types here mean

- classes
- interfaces

E.g. `java.lang` is package with basec classes of java, `java.io` is package with reading and writing classes

# Creating package

First, you have to decide on package name. You have to mension package name in each file which is to be included in that package.

```java
package com.example.className;
```

It must be first line of file. Each file can belong to only one package which means we can't write above line more than once in file.

When you don't mension it then that file belongs to unnamed package.

# Naming package

- Package name are written in lower case.
- You can use reversed domain name of your company
  E.g. `com.exmpaleCompany.package`;
  - To avoid naming conflict in same company, project name is also included.
- If any part of package name is having more than two words then you can use underscore to separate. Underscore can also be used to resolve if package name contains reserce keyword of java.

> classes included in package are called package member

# Using package

## Fully qualified name

You can refere to class in particular package by using package name followed by class name.

Suppose you have your own math class then you can use that class like `com.example.project.Math`. Here `Math` is class name of package `com.example.project`.

```java
com.example.project.Math m = new com.example.project.Math();
```

## Importing class from package.

You can use `import` statement to import the particular class from some package. But it should be after `package` statement.

Syntax - `import package.name;`

If you are in same package the you don't need to import. But if you are refering to some other class some other package then you need to import. Suppose from above example, if you are using math class frequently in your program. It becomes tedious to refer to that class using fully qualified name each time. It is better to use that `import` statement that time.

E.g.

```java
import com.example.Math
```

## Importing entier package

If you are using many classe out of same package, it is better to import the entier package.

```java
import com.example.*;
```

## Importing nested classes

You can import particular or all nested classes of particular class.

```java
import com.example.Math.Circle;
import com.example.Math.*;
```

**This won't import the Math class, you have to import it separately**

## static import

You can use static impor to import static member of the class. In case of `java.lang.Math`, you can import like `import java.lang.Math.*` to import all the static methods. After this you won't need use `Math.` to refer to any method.

```java
import static java.lang.Math.*;
import static java.lang.Math.PI;
```
