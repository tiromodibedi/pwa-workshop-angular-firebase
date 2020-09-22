# Step 3 - Customize app icons and splash screens

In this step, we're going to customize our app's native look and feel on multiple platforms. When added PWA schematic of Angular, we've had automatically generated icon files under `/src/assets/icons` folder. 

We're going to replace those icons with our own assets. We will generate splash screens for iOS platform and add meta tags required to declare them to `index.html` file. We also need to update `manifest.webmanifest` file to declare our new icons.

## Remove default assets

First of all, we need to remove default icons generated by @angular/pwa schematic.

Navigate to `/src/assets` folder and remove `icons` folder there. 

We also need to update `manifest.webmanifest` file. Open `src/manifest.webmanifest` file and empty `icons` array. Eventually your manifest file has to look like this;

```json
{
  "name": "Conference App",
  "short_name": "Conf App",
  "theme_color": "#387ef5",
  "background_color": "#ffffff",
  "display": "standalone",
  "scope": "/",
  "start_url": "/?utm_source=home_screen",
  "description": "This is a dummy Angular app which demonstrates a PWA's behaviour on different platforms.",
  "icons": [
  ]
}
```

## Generate new icons and splash screen images

We are going to use a library to automatically generate icons and splash screens for us. But first, let's see the requirements.

### Declaring icons and splash screens on iOS

Although many browsers adapted the [Web App Manifest spec](https://w3c.github.io/manifest/), WebKit (specifically, Mobile Safari on iOS) currently uses custom non-standards track meta tag implementations.

We need to add special non-standard meta tags - [see here](https://developer.apple.com/library/archive/documentation/AppleApplications/Reference/SafariWebContent/ConfiguringWebApplications/ConfiguringWebApplications.html) in order to have our PWAs display splash screens and icons on iOS.

iOS requires an image and corresponding html tag per device resolution and orientation. Here's an example html tag for declaring a splash screen for just 1 device resolution and orientation. 

```html
<link rel="apple-touch-startup-image" href="assets/pwa/apple-splash-2048-2732.png" media="(device-width: 1024px) and (device-height: 1366px) and (-webkit-device-pixel-ratio: 2) and (orientation: portrait)">
```

If the size of an image in the meta tag matches with the device’s resolution, iOS will show the image as a splash screen. Here’s a list of devices and their resolutions: https://developer.apple.com/design/human-interface-guidelines/ios/icons-and-images/launch-screen/#static-launch-screen-images-not-recommended

![Static launch screen images](https://cdn-images-1.medium.com/max/1600/1*hKRjSlhCNrFMo0ut_O9RBg.png) 

A special html tag is also required to display app icons on iOS. 

```html
<link rel="apple-touch-icon" sizes="180x180" href="assets/pwa/apple-icon-180.png">
```

We need to create static images in different sizes for different devices and orientations. Creating icon and splash screen images for all the platforms, maintaining sizes and quality for all and adding HTML tags for each image can be overwhelming. That's why we're going to automate this instead.

### Automating the image generation

I created a CLI library to automate all the details described above. It generates images for splash screens and icons targeting multiple platforms at once, updating your `index.html` and `manifest.webmanifest` files accordingly. 
 
Run `npm run resources` command. And, all image assets will be generated for you. Library also updates your `index.html` and `manifest.webmanifest` files for declaring your generated assets.  

Eventually, you should see the following code in `index.html` file of your PWA. You also can see the generated images on `src/assets/pwa` folder.

```html
<link rel="apple-touch-icon" sizes="180x180" href="assets/pwa/apple-icon-180.png">
<link rel="apple-touch-icon" sizes="167x167" href="assets/pwa/apple-icon-167.png">
<link rel="apple-touch-icon" sizes="152x152" href="assets/pwa/apple-icon-152.png">
<link rel="apple-touch-icon" sizes="120x120" href="assets/pwa/apple-icon-120.png">

<meta name="apple-mobile-web-app-capable" content="yes">

<link rel="apple-touch-startup-image" href="assets/pwa/apple-splash-2048-2732.png" media="(device-width: 1024px) and (device-height: 1366px) and (-webkit-device-pixel-ratio: 2) and (orientation: portrait)">
<link rel="apple-touch-startup-image" href="assets/pwa/apple-splash-2732-2048.png" media="(device-width: 1024px) and (device-height: 1366px) and (-webkit-device-pixel-ratio: 2) and (orientation: landscape)">
<link rel="apple-touch-startup-image" href="assets/pwa/apple-splash-1668-2388.png" media="(device-width: 834px) and (device-height: 1194px) and (-webkit-device-pixel-ratio: 2) and (orientation: portrait)">
<link rel="apple-touch-startup-image" href="assets/pwa/apple-splash-2388-1668.png" media="(device-width: 834px) and (device-height: 1194px) and (-webkit-device-pixel-ratio: 2) and (orientation: landscape)">
<link rel="apple-touch-startup-image" href="assets/pwa/apple-splash-1668-2224.png" media="(device-width: 834px) and (device-height: 1112px) and (-webkit-device-pixel-ratio: 2) and (orientation: portrait)">
<link rel="apple-touch-startup-image" href="assets/pwa/apple-splash-2224-1668.png" media="(device-width: 834px) and (device-height: 1112px) and (-webkit-device-pixel-ratio: 2) and (orientation: landscape)">
<link rel="apple-touch-startup-image" href="assets/pwa/apple-splash-1536-2048.png" media="(device-width: 768px) and (device-height: 1024px) and (-webkit-device-pixel-ratio: 2) and (orientation: portrait)">
<link rel="apple-touch-startup-image" href="assets/pwa/apple-splash-2048-1536.png" media="(device-width: 768px) and (device-height: 1024px) and (-webkit-device-pixel-ratio: 2) and (orientation: landscape)">
<link rel="apple-touch-startup-image" href="assets/pwa/apple-splash-1242-2688.png" media="(device-width: 414px) and (device-height: 896px) and (-webkit-device-pixel-ratio: 3) and (orientation: portrait)">
<link rel="apple-touch-startup-image" href="assets/pwa/apple-splash-2688-1242.png" media="(device-width: 414px) and (device-height: 896px) and (-webkit-device-pixel-ratio: 3) and (orientation: landscape)">
<link rel="apple-touch-startup-image" href="assets/pwa/apple-splash-1125-2436.png" media="(device-width: 375px) and (device-height: 812px) and (-webkit-device-pixel-ratio: 3) and (orientation: portrait)">
<link rel="apple-touch-startup-image" href="assets/pwa/apple-splash-2436-1125.png" media="(device-width: 375px) and (device-height: 812px) and (-webkit-device-pixel-ratio: 3) and (orientation: landscape)">
<link rel="apple-touch-startup-image" href="assets/pwa/apple-splash-828-1792.png" media="(device-width: 414px) and (device-height: 896px) and (-webkit-device-pixel-ratio: 2) and (orientation: portrait)">
<link rel="apple-touch-startup-image" href="assets/pwa/apple-splash-1792-828.png" media="(device-width: 414px) and (device-height: 896px) and (-webkit-device-pixel-ratio: 2) and (orientation: landscape)">
<link rel="apple-touch-startup-image" href="assets/pwa/apple-splash-1242-2208.png" media="(device-width: 414px) and (device-height: 736px) and (-webkit-device-pixel-ratio: 3) and (orientation: portrait)">
<link rel="apple-touch-startup-image" href="assets/pwa/apple-splash-2208-1242.png" media="(device-width: 414px) and (device-height: 736px) and (-webkit-device-pixel-ratio: 3) and (orientation: landscape)">
<link rel="apple-touch-startup-image" href="assets/pwa/apple-splash-750-1334.png" media="(device-width: 375px) and (device-height: 667px) and (-webkit-device-pixel-ratio: 2) and (orientation: portrait)">
<link rel="apple-touch-startup-image" href="assets/pwa/apple-splash-1334-750.png" media="(device-width: 375px) and (device-height: 667px) and (-webkit-device-pixel-ratio: 2) and (orientation: landscape)">
<link rel="apple-touch-startup-image" href="assets/pwa/apple-splash-640-1136.png" media="(device-width: 320px) and (device-height: 568px) and (-webkit-device-pixel-ratio: 2) and (orientation: portrait)">
<link rel="apple-touch-startup-image" href="assets/pwa/apple-splash-1136-640.png" media="(device-width: 320px) and (device-height: 568px) and (-webkit-device-pixel-ratio: 2) and (orientation: landscape)">
```

You should also see the following new icons in your manifest.webmanifest files' icons array.

```json
{
  "icons": [
    {
      "src": "assets/pwa/manifest-icon-192.png",
      "sizes": "192x192",
      "type": "image/png",
      "purpose": "any"
    },
    {
      "src": "assets/pwa/manifest-icon-512.png",
      "sizes": "512x512",
      "type": "image/png",
      "purpose": "any"
    }
  ]
}
```

Please verify all the changes before proceeding.

> Keep an eye on WebKit Feature Status for tracking the progress of the implementation of web standards. For instance; once Web App Manifest specs is implemented on WebKit, you won’t need to use the custom meta tags above anymore. Track the progress here: https://webkit.org/status/#?search=manifest

If you like the library, please star it on GitHub and follow the developments on it: https://github.com/onderceylan/pwa-asset-generator

## Add meta tags for the status bar on iOS

You can customize iOS status bar of your PWA by using `apple-mobile-web-app-status-bar-style` meta tag in your index.html file. This meta tag has no effect unless you specify full-screen mode aka standalone for your PWA.

View of the status bars; `black-translucent`, `white`, and `black`;

![View of the status bars](https://cdn-images-1.medium.com/max/1600/1*DmaoahB1qXMpZgt2X2gq9Q.png)

Add the following meta tag to your index.html file;

```html
<meta name="apple-mobile-web-app-status-bar-style" content="black-translucent">
```

## Test the results

Once you're done with the instructions, you can test it by building the app for production. 

Run `npm run build:serve` to spin off an http server for your production build. Open `http://127.0.0.1:8080` in your browser to inspect the web app manifest with the new logos.

## Good to go 🎯
Now you can continue to Step 4 -> [Display A2HS on iOS](https://github.com/onderceylan/pwa-workshop-angular-firebase/blob/step-4/README.md). 
