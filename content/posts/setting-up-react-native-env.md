---
title: 'Problems while setting Up React Native developer environment'
date: 2022-10-18T18:21:01+05:30
draft: false
tags:
  - react-native
---

# Build failed. Failed to execute the installDebug command in android.

This problem happens mainly when your virtual device is running less on memory and is trying to install new build but failing because of insufficient storage.

**To solve this -**

- Uninstall the previous build and try running build again.
- Wipe the data of virtual device
  1.  You can do this by going to virtual device manager.
  2.  Then Click vertical ellipsis symbol.
  3.  Click on option to wipe data.
- If above steps doesn't work then re-create the virtual device.

**To avoid this problem -**

- While createing the virtual device assign some more memory to virtual device by going to advance setting on create virtual device window where it shows all the details of virtual device to be created.

!()[/static/images/problems-while-setting-up-react-native-dev-env/virtual-device-manager.png]

# Ruby version while setting up dev environment for ios project in macOS

Cocoapod is package manager which is used to setup the ios project in react native. To install the necessary dependency, it requires ruby version given [here](https://github.com/facebook/react-native/blob/main/template/_ruby-version).

You can install that by

1. Install ruby version manager
   ```sh
   brew install rbenv
   ```
2. Install require version
   ```sh
   rbenv install 2.7.6
   ```
3. Check installation by executin

   ```sh
   ruby --version
   ```

   If it is not showing given version after installation, follow next steps.

Go to configuration file of your shell. Paste following command.

```sh
export PATH="$HOME/.rbenv/bin:$PATH" # to point to newly installed ruby directory
eval "$(rbenv init -)" # to initialise the rbenv on shell startup. Not needed.
```
