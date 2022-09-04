---
title: 'Jar Files in Java'
date: 2022-09-03T15:18:53+05:30
draft: false
tags:
  - java
---

# JAR file (Java Archive)

JAR file is used to bundle the software files. This makes it easier to send across the devices and run it without hussle.

### Syntax

```sh
jar {ctxui}[vfmn0PMe] [jar-file] [manifest-file] [entry-point] [-C dir] files ...
```

### Options

- `c` : Create jar file.
- `t` : Print content of jar file.
- `C` : Change to specified directory.
- `e` : To indicate that entry point is mensioned in command.
- `x` : To extract the files from jar file.
- `u` : To update the existing archive.
- `m` : To specify the manifest file path.

E.g.

```sh
jar cfe shapes.jar com.tw.step.graphics.ShapesMain -C out .
```

- Here as e option is specified, the entry point `com.tw.step.graphics.ShapesMain` of program where main function resides, is mensioned.
  `shapes.jar` is name of jar file.
- `-C out .` specfies that out is directory where class files are present. -C option makes jar file go to that directory, the path `.` is used inside that directory.

# Manifest file

Every file have only one manifest file under path `MANIFEST.MF`. This file contains information about archive and files included in archive. It can include the entry point (main function's class), classpath etc.

Entries in manifest file are in form of `header: value`.
