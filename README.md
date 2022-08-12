# Lonely Island Note

A note app Built by Cordova and jQuery.
![logo-no-bg](https://user-images.githubusercontent.com/13687360/161952348-f4d19fee-df7d-4157-9113-6ef96cbef0f2.png)


# Documentation

## Plugins

Check Plugins installed:

```shell
cordova plugin ls
```

Install a new plugin:

```shell
cordova plugin add <PLUGIN_NAME>
```

Remove a plugin:

```shell
cordova plugin rm <PLUGIN_NAME>
```

Update a plugin:

```shell
cordova plugin update <PLUGIN_NAME>
```

## Documentation from Cordova

Visit link below to check full CLIs for Cordova:
https://cordova.apache.org/docs/en/11.x/reference/cordova-cli/index.html

## File System

- Reference0: https://cordova.apache.org/docs/en/11.x/reference/cordova-plugin-file/index.html
- Reference1: https://www.w3.org/TR/2012/WD-file-system-api-20120417/
- Reference2: https://www.w3.org/TR/FileAPI

## QR Scanner

https://github.com/bitpay/cordova-plugin-qrscanner

## Image Picker

https://github.com/DmcSDK/cordova-plugin-mediaPicker

## File Opener

https://github.com/pwlin/cordova-plugin-file-opener2

## Message Box

https://github.com/apache/cordova-plugin-dialogs

## Zipper

https://github.com/jjdltc/jjdltc-cordova-plugin-zip

## Encryptor

https://github.com/Ideas2IT/cordova-aes256

# Environment

```shell
export ANDROID_SDK_ROOT=/Users/linxiaozhou/Library/Android/sdk
```

# Debug in device

Enable Developer mode in device, then run command below:

```shell
cordova run android --device
```

## JDK 1.8 requirements

If you don't want to change your JDK version from current to 1.8.x, follow this step after add platform android and before build:

- Open file in `platforms/android/cordova/lib/check_reqs.js`
- Change code in funtion `module.exports.run = function (){}`

```javascript
// Returns a promise.
module.exports.run = function () {
  return Q.all([this.check_java(), this.check_android()]).then(function (
    values
  ) {
    console.log("Checking Java JDK and Android SDK versions");
    console.log(
      "ANDROID_SDK_ROOT=" +
        process.env["ANDROID_SDK_ROOT"] +
        " (recommended setting)"
    );
    console.log(
      "ANDROID_HOME=" + process.env["ANDROID_HOME"] + " (DEPRECATED)"
    );

    if (!String(values[0]).startsWith("1.8.")) {
      // Edit here
      throw new CordovaError(
        "Requirements check failed for JDK 8 ('1.8.*')! Detected version: " +
          values[0] +
          "\n" +
          "Check your ANDROID_SDK_ROOT / JAVA_HOME / PATH environment variables."
      );
    }

    if (!values[1]) {
      throw new CordovaError(
        "Requirements check failed for Android SDK! Android SDK was not detected."
      );
    }
  });
};
```

Reference: https://blog.csdn.net/sunwe/article/details/106295073

# Build

```shell
yarn build

// Or
cordova build
```

# Config

To Config app info, edit this file: `./config.xml`

# Icons

To change Icons for Android, follow this link: [Customize Icons](https://cordova.apache.org/docs/en/11.x/config_ref/images.html)

# Http Protocal Banned

Add this tag in `config.xml` to enable http protocol:

```xml
<edit-config file="AndroidManifest.xml" mode="merge" target="/manifest/application" xmlns:android="http://schemas.android.com/apk/res/android">
  <activity android:usesCleartextTraffic="true" />
</edit-config>
```

Please note that this attribute must be added in new tag:

```plaintext
xmlns:android="http://schemas.android.com/apk/res/android"
```

Ref: https://www.cnblogs.com/muzhe/articles/13213047.html
