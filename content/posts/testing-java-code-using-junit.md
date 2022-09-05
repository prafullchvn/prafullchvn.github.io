---
title: 'Testing Java Code Using Junit'
date: 2022-09-04T11:37:32+05:30
draft: false
tags:
  - java
---

## Conecpts

**Container**

A node in test tree that contains other tests or container

**Test**

A method in test tree that checks the assertion.

**Life Cycle methods**

Methods which are executed at particular moment of execution of tree node. Generall they are marked using `@BeforeEach`, `@AfterEach`, `@BeforeAll` and `@AfterAll`.

**Test Class**

Any top-level class, static member class or nested class that contains at least one method i.e. container. Test classes must not be abstract and must have a single constructor.

**Test Method**

Any method that is annoted with `@Test`, `@RepeatedTest`, `@ParameterizedTest`, `@TestFactory` or `@TestTemplate`. Except `@Test`, other groups tests, in case of `@TestFactory` it creates container.

## Directory structure

For this article, I am goint to follow the following directory structure.

```sh
├── out
│   ├── src
│   └── test
├── src
│   └── com
│       └── tw
│           └── step
│               └── date
└── test
    └── com
        └── tw
            └── step
                └── date
```

## Writing test

As given above, we are going to have same structure in test directory as we have in src directory.

To run the tests, we need to import static `assertEquals` function from Assertions. We need to mark the function as test using annotation `@Test` provided in junit.

```java
package com.tw.step.date;

import static org.junit.jupiter.api.Assertions.assertEquals;
import org.junit.jupiter.api.Test;


class DateTest{
  @Test
  public void getNoOfDaysInJanuary(){
    int expectedDays = 31;
    int month = 1;
    int year = 2022;

    assertEquals(Date.noOfDaysInMonth(month, year), expectedDays);
  }
}
```

## Compiling test

To compile the test we need to do tell somethings to `javac` command. Those are

1. `sourcepath` of test
2. `classpath` of junit library and src
3. file where test class resides
4. path where test class files should be generated

```sh
javac -sourcepath test -classpath "lib/junit-platform-console-standalone-1.9.0.jar:out/src" test/com/tw/step/date/DateTest.java  -d out/test
```

**Here**

- `-sourcepath test` is java file of test resides
- `-classpath "lib/junit-platform-console-standalone-1.9.0.jar:out/src" ` junit is package which we are using to test.
  `out/src` is path where class file being tested resides.
- `test/com/tw/step/date/DateTest.java` is file where test class is craeted.
- `-d out/test` is path where class file of test will be generated.

## Running the test

For running test we need to execute console launcher of junit package and tell it where all the class files reside.
Console.launcher will analyse all test file and look for all the function marked as test.

```sh
java -jar "lib/junit-platform-console-standalone-1.9.0.jar" -cp "out/test:out/src" -p "com.tw.step.date"
```

Here

- `-jar "lib/junit-platform-console-standalone-1.9.0.jar"` is used to tell which junit package to execute.
- `-cp "out/test:out/src"` is used to tell where can it find test class files and src class files.
- `-p "com.tw.step.date"` is used to tell package to it should look for.

### Executing two packages simultaneously

In case where if there are two packages that need to be compied then you can compile them by adding path of file in `javac` command adding there dependency in `classpath` as well.

```sh
javac -sourcepath test -cp "lib/junit-package.jar:lib/someotherdependency.jar:out/src" -d out/test test/com/tw/step/package1/FileTest.java test/com/tw/step/package2/FileTest.java
```

Using find command

```sh
find test -name "*.java" -exec javac -sourcepath test -cp "lib/junit-platform-console-standalone-1.9.0.jar:lib/date.jar:out/src" -d out/test {} \;
```

To execute, use same command by adding necessary dependency in `classpath`.

```sh
java -jar junit-package.jar -cp "out/test:out/src" -p com
```

Here it searches all files with package starting with `com`.

## Points to Rembember

- You have to mension the path where src class file is stored both in compilation and execution test.
- Remember to use put package name same in both source and test files.

## References

[Junit package](https://search.maven.org/artifact/org.junit.platform/junit-platform-console-standalone/1.9.0/jar)

[Junit Docs](https://search.maven.org/artifact/org.junit.platform/junit-platform-console-standalone/1.9.0/jar)

[Junit console launcher docs](https://search.maven.org/artifact/org.junit.platform/junit-platform-console-standalone/1.9.0/jar)

[Assertions](https://junit.org/junit5/docs/5.0.1/api/org/junit/jupiter/api/Assertions.html)
