---
title: 'Debugging in Chrome'
date: 2022-09-01T18:38:52+05:30
draft: false
tags:
  - debugging
---

How to debug in chrome? Most obvious answer will be `console.log`.
But writing console.log all over the places can get messy.

But there are some easy ways to do that.

# Live Expression

Open DevTools > Go to console tab > click on eye like symbol

![](/images/debugging-in-chrome/live-expression-eye-symbol.png)

Type expressin that you wanna watch. This expression will be maintained for all the site you visit. Instead of flooding your console it will show the live value.

# Debugging Tool

Open DevTools > Go to source tab > Open js file that you wanna debug.
There you can add breakpoint to line you wanna stop flow.

There are three button.

![](/images/debugging-in-chrome/debug-panel-buttons.png)

### Continue

This button is used to continue the flow after breakpoint is hit.

![](/images/debugging-in-chrome/continue-pause.png)

### Step over

This button is used to execute the current line and move to next line.

![](/images/debugging-in-chrome/step-over.png)

### Step Into

This button is used to step into the function to which function call is made.

![](/images/debugging-in-chrome/step-into.png)

### Step Out

This button is used to step out of current functin execution onto the next line after function call.

![](/images/debugging-in-chrome/step-out.png)

In right side, you will find Scope which will have all the variables currently in scope of the line where you have place breakpoint or where debugger has paused flow.

Here you can add break point on event also or if some node changes.

Under watch you can type your expression of which you want to check value.

![](/images/debugging-in-chrome/chrome-debug-right-side-panel.png)
