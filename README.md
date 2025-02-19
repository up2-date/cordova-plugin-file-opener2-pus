# A File Opener Plugin for Cordova

This plugin will open a file on your device file system with its default application.

```js
cordova.plugins.fileOpener2.open(
    filePath,
    fileMIMEType,
    {
        error : function(){ },
        success : function(){ }
    }
);
```

## Installation

```shell
$ cordova plugin add github:up2-date/cordova-plugin-file-opener2-pus
```

### Optional variables

This plugin requires the Android support library v4. From release `2.1.0` the version of this can be set at installation. The minimum version is `24.1.0`. Default value is `27.+`. [Check out the latest version](https://developer.android.com/topic/libraries/support-library/revisions.html).

```shell
$ cordova plugin add github:up2-date/cordova-plugin-file-opener2-pus  --variable ANDROID_SUPPORT_V4_VERSION="27.+"
```

If you are using the `cordova-android-support-gradle-release` plugin it should match the value you have set there.

## Requirements

The following platforms and versions are supported by the latest release:

- Android 4.4+ / iOS 9+ / Electron
- Cordova CLI 7.0 or higher

Cordova CLI 6.0 is supported by 2.0.19, but there are a number of issues, particularly with Android builds (see [232](https://github.com/pwlin/cordova-plugin-file-opener2/issues/232) [203](https://github.com/pwlin/cordova-plugin-file-opener2/issues/203) [207](https://github.com/pwlin/cordova-plugin-file-opener2/issues/207)). Using the [cordova-android-support-gradle-release](https://github.com/dpa99c/cordova-android-support-gradle-release) plugin may help.

### AndroidX Support

Currently if your project requires AndroidX support, you need to add the following two plugins to your project:

- [cordova-plugin-androidx](https://github.com/dpa99c/cordova-plugin-androidx/) and [cordova-plugin-androidx-adapter](https://github.com/dpa99c/cordova-plugin-androidx-adapter/)
```shell
$ cordova plugin add cordova-plugin-androidx
$ cordova plugin add cordova-plugin-androidx-adapter
```
Just adding these plugins should be enough and no further changes are necessary.


## fileOpener2.open(filePath, mimeType, options)

Opens a file

### Supported Platforms

- Android 4.4+
- iOS 9+
- Electron

### Quick Examples
Open a PDF document with the default PDF reader and optional callback object:

```js
cordova.plugins.fileOpener2.open(
    '/Download/starwars.pdf', // You can also use a Cordova-style file uri: cdvfile://localhost/persistent/Downloads/starwars.pdf
    'application/pdf',
    {
        error : function(e) {
            console.log('Error status: ' + e.status + ' - Error message: ' + e.message);
        },
        success : function () {
            console.log('file opened successfully');
        }
    }
);
```

__Note on Electron:__ Do not forget to enable Node.js in your app by adding `"nodeIntegration": true` to `platforms/electron/platform_www/cdv-electron-settings.json` file, See [Cordova-Electron documentation](https://cordova.apache.org/docs/en/latest/guide/platforms/electron/index.html#customizing-the-application's-window-options).

### Market place installation
Install From Market: to install an APK from a market place, such as Google Play or the App Store, you can use an `<a>` tag in combination with the `market://` protocol:

```html
<a href="market://details?id=xxxx" target="_system">Install from Google Play</a>
<a href="itms-apps://itunes.apple.com/app/my-app/idxxxxxxxx?mt=8" target="_system">Install from App Store</a>
```
or in code:

```js
window.open("[market:// or itms-apps:// link]","_system");
```

## fileOpener2.showOpenWithDialog(filePath, mimeType, options)

Opens with system modal to open file with an already installed app.

### Supported Platforms

- Android 4.4+
- iOS 9+

### Quick Example

```js
cordova.plugins.fileOpener2.showOpenWithDialog(
    '/Downloads/starwars.pdf', // You can also use a Cordova-style file uri: cdvfile://localhost/persistent/Downloads/starwars.pdf
    'application/pdf',
    {
        error : function(e) {
            console.log('Error status: ' + e.status + ' - Error message: ' + e.message);
        },
        success : function () {
            console.log('file opened successfully');
        },
        position : [0, 0]
    }
);
```
`position` array of coordinates from top-left device screen, use for iOS dialog positioning.

---

## SD card limitation on Android

It is not always possible to open a file from the SD Card using this plugin on Android. This is because the underlying  Android library used [does not support serving files from secondary external storage devices](https://stackoverflow.com/questions/40318116/fileprovider-and-secondary-external-storage). Whether or not your the SD card is treated as a secondary external device depends on your particular phone's set up.

---

## Notes

- For properly opening _any_ file, you must already have a suitable reader for that particular file type installed on your device. Otherwise this will not work.

- [It is reported](https://github.com/pwlin/cordova-plugin-file-opener2/issues/2#issuecomment-41295793) that in iOS, you might need to remove `<preference name="iosPersistentFileLocation" value="Library" />` from your `config.xml`

- If you are wondering what MIME-type should you pass as the second argument to `open` function, [here is a list of all known MIME-types](http://svn.apache.org/viewvc/httpd/httpd/trunk/docs/conf/mime.types?view=co)


---
