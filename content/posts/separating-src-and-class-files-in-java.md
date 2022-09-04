---
title: 'Separating Src and Class Files in Java'
date: 2022-09-03T15:54:33+05:30
draft: false
tags:
  - java
---

# src directory

It is directory where all the `.java` file are stored. Generally in structure which your package should follow.

# out directory

It is directory where all the `.class` file are stored. It also follows structure of package.

Example

```sh
├── out
│   └── com
│       └── tw
│           └── step
│               └── graphics
│                   ├── Canvas.class
│                   ├── ShapesMain.class
│                   └── shapes
│                       ├── Circle.class
│                       └── Rectangle.class
├── shapes.jar
└── src
    └── com
        └── tw
            └── step
                └── graphics
                    ├── Canvas.java
                    ├── ShapesMain.java
                    └── shapes
                        ├── Circle.java
                        └── Rectangle.java
```

# How to separate

## Compiling

While compiling use follow following structure.

`javac -sourcepath source_dir /path/to/file/with/mainFunction.java -d dest_dir`

- Here `-sourcepath` is used to mension the directory where java files start i.e. source_dir.
- Then you have to mension the entry point file of program.
- `-d dest_dir` is used to specify the destination directory where class file will be generated with same structure as source. Destination directory should already be created.

Example

```sh
javac -sourcepath src src/com/tw/step/graphics/ShapesMain.java -d out
```

## Executing

While executing you follow following structure.

`java -cp class_dir com.example.project.Main`

- Here cp is used to mension the class directory where all the class files reside.
- You need to mension class where main function resides.

Example

```sh
java -cp out com.tw.step.graphics.ShapesMain
```
