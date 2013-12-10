# Apache Cordova Facebook Plugin

This is the official plugin for Facebook in Apache Cordova/PhoneGap!

The Facebook plugin for [Apache Cordova](http://incubator.apache.org/cordova/) allows you to use the same JavaScript code in your Cordova application as you use in your web application. However, unlike in the browser, the Cordova application will use the native Facebook app to perform Single Sign On for the user. If this is not possible then the sign on will degrade gracefully using the standard dialog based authentication.

## Facebook Requirements and Set-Up

The Facebook SDK (both native and JavaScript) is changing independent of this plugin. The manual install instructions include how to get the latest SDK for use in your project.

To use this plugin you will need to make sure you've registered your Facebook app with Facebook and have an APP_ID (https://developers.facebook.com/apps).

If you plan on rolling this out on iOS, please note that you will need to ensure that you have properly set up your Native iOS App settings on the [Facebook App Dashboard](http://developers.facebook.com/apps). Please see the [Facebook SDK for iOS](https://developers.facebook.com/docs/ios).

If you plan on rolling this out on Android, please note that you will need to [generate a hash of your Android key(s) and submit those to the Developers page on Facebook](https://developers.facebook.com/docs/android) to get it working. Furthermore, if you are generating this hash on Windows (specifically 64 bit versions), please use version 0.9.8e or 0.9.8d of [OpenSSL for Windows](http://code.google.com/p/openssl-for-windows/downloads/list) and *not* 0.9.8k. Big ups to [fernandomatos](http://github.com/fernandomatos) for pointing this out!

# Project Structure

`www/facebook-connect-debug.js` is the modified facebook-js-sdk. It already includes the hooks to work with this plugin.

`www/pg-plugin-fb-connect.js` is the JavaScript code for the plugin, this defines the JS API.

`src/android` and `src/ios` contain the native code for the plugin for both Android and iOS platforms.

## Phonegap 3.1.0 or greater installation

1. Installed the plugin using phonegap plugin tools

```
phonegap local plugin add https://github.com/mallzee/phonegap-facebook-plugin.git
```

2. Install the iOS and/or Android Facebook SDKs (to be elaborated upon)

3. Update the configuration (to be elaborated upon)

```JavaScript
if (phonegap.isEnabled()) {
  document.addEventListener('deviceready', function () {
    FB.init({
      appId: FBAPPID,                 // App ID from the app dashboard
      nativeInterface: CDV.FB,
      useCachedDialogs: false
    });
  }, false);
} else {
  window.fbAsyncInit = function() {
    FB.init({
      appId: FBAPPID                  // App ID from the app dashboard
    });
  };

  // Load the SDK asynchronously
  (function(d, s, id){
    var js, fjs = d.getElementsByTagName(s)[0];
    if (d.getElementById(id)) {return;}
    js = d.createElement(s); js.id = id;
    js.src = "//connect.facebook.net/en_US/all.js";
    fjs.parentNode.insertBefore(js, fjs);
  }(document, 'script', 'facebook-jssdk'));
}
```
