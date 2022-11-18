---
title: 'Codepush Setup for Android'
date: 2022-11-17T10:50:21+05:30
draft: false
tags:
  - codepush
  - react-native
---

Codepush is feature that allows to make changes in code on live application.

- Codepush is microsoft solution to update code.
- Only JS code (in case of React Native).
- Fastest way to apply quick changes
- Codepush supports React Native.
- In Case of react native, using codepush we can make changes in JS code only.

![](/images/codepush-setup/codepush.jpeg)

Setting up Codepush

In order to implement there are 4 broader steps.

1.  Create app on app center.
2.  Implement SDK in project.
3.  Uploading changes to app center.

Before diving deeper in installation, you need react-native version 69 or lower for codepush to work.

1.  Create app on app center. Go to [appcenter](https://appcenter.ms).
2.  Click on `Add New` on dashboard.

![](/images/codepush-setup/appcenter-dashboard.png)

i. Click on `Add new App`'

ii. Select the platform as android (for now will setup for android).

iii. Select OS as android and platform as React Native.

iv. For `Release Type` you can give it anything as per you need.

    ![](/images/codepush-setup/selecting-platform.png)

3.  After creation of app it will display some steps that you need to follow.
    Those steps will look like given in following image. Go through the steps.

    In 3rd step there will be given the app secret key which you need to post it in file created in 2nd step. 4th step is just telling you to expore the platform.

    ![](/images/codepush-setup/sdk-setup-steps.png)

4.  Android setup

### Plugin Installation and Configuration for React Native 0.60 version and above (Android)

i. In your `android/settings.gradle` file, make the following additions at the end of the file:

```gradle
...
include ':app', ':react-native-code-push'
project(':react-native-code-push').projectDir = new File(rootProject.projectDir, '../node_modules/react-native-code-push/android/app')
```

ii. In your `android/app/build.gradle` file, add the `codepush.gradle` file as an additional build task definition underneath `react.gradle`:

```gradle
...
apply from: "../../node_modules/react-native/react.gradle"
apply from: "../../node_modules/react-native-code-push/android/codepush.gradle"
...
```

iii. Update the `MainApplication.java` file to use CodePush via the following changes:

```java
...
// 1. Import the plugin class.
import com.microsoft.codepush.react.CodePush;

public class MainApplication extends Application implements ReactApplication {

    private final ReactNativeHost mReactNativeHost = new ReactNativeHost(this) {
        ...

        // 2. Override the getJSBundleFile method in order to let
        // the CodePush runtime determine where to get the JS
        // bundle location from on each app start
        @Override
        protected String getJSBundleFile() {
            return CodePush.getJSBundleFile();
        }
    };
}
```

iv. Add the Deployment key to `strings.xml`:

To let the CodePush runtime know which deployment it should query for updates, open your app's `strings.xml` file and add a new string named `CodePushDeploymentKey`, whose value is the key of the deployment you want to configure this app against (like the key for the `Staging` deployment for the `FooBar` app). You can retrieve this value by running `appcenter codepush deployment list -a <ownerName>/<appName> -k` in the CodePush CLI (the `-k` flag is necessary since keys aren't displayed by default) and copying the value of the `Key` column which corresponds to the deployment you want to use (see below). Note that using the deployment's name (like Staging) will not work. The "friendly name" is intended only for authenticated management usage from the CLI, and not for public consumption within your app.

![Deployment list](https://cloud.githubusercontent.com/assets/116461/11601733/13011d5e-9a8a-11e5-9ce2-b100498ffb34.png)

In order to effectively make use of the `Staging` and `Production` deployments that were created along with your CodePush app, refer to the [multi-deployment testing](../README.md#multi-deployment-testing) docs below before actually moving your app's usage of CodePush into production.

Your `strings.xml` should looks like this:

```xml
 <resources>
     <string name="app_name">AppName</string>
     <string moduleConfig="true" name="CodePushDeploymentKey">DeploymentKey</string>
 </resources>
```

_Note: If you need to dynamically use a different deployment, you can also override your deployment key in JS code using [Code-Push options](./api-js.md#CodePushOptions). If you are using version lower than 60 then there are some more steps that you need to follow._

4. After doing this Go to `Distrubte -> Codepush -> Click on Create Standard Deployment`

5. After creating Create Standard Deployment, you will see some steps.

![](/images/codepush-setup/setting-up-distribution.png)

i. Install `appcenter-cli` that is how you will be publishing the changes to codepush.

ii. Step 2 we already did.

iii. For step 3 we can just create build with signing config.

iv. Command given in step 4 is use to publish the changes to appcenter

```sh
appcenter codepush release-react -a <user-name>/<app name> -d Staging
```
