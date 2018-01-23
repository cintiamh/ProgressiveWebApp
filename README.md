# ProgressiveWebApp
Following https://codelabs.developers.google.com/codelabs/your-first-pwapp/#0

## What you'll need

* Latest Chrome
* [Web Server for Chrome](https://chrome.google.com/webstore/detail/web-server-for-chrome/ofhbbkphhbklhfoeikjpcbhemlocgigb), or any web server
* [Chrome Dev Tools](https://developer.chrome.com/devtools)

## Architect your App Shell

Minimal HTML, CSS and JavaScript to power PWA's UI for good performance.

First load should be quick and immediately cached.

Separate the core application infrastructure and UI from the data.

Service worker: script running on the background, opening the door to features not related to page interaction.

* What needs to be on screen immediately?
* What other UI components are key to our app?
* What supporting resources are needed for the app shell? (JS, styles, etc)

## Implement your App Shell

skeleton: web starter kit https://developers.google.com/web/tools/starter-kit/

## Start with a fast first load

`localStorage` can be slow and not ideal for production.

Instead try to use [idb](https://www.npmjs.com/package/idb). Take a look into [localForage](https://github.com/localForage/localForage).

## Use service workers to pre-cache the App Shell

Read about service workers: https://developers.google.com/web/fundamentals/primers/service-workers/

### Register the service worker if it's available

Register a service worker to make the app work offline:

1. tell the browser to register the JavaScript file as the service worker.
2. create a JavaScript file containing the service worker.

Chrome Dev Tools: Application Panel => Service Worker Pane.

While developing, check the "Update on reload" option.

### Test it out

Google Dev Tools => Application => Cache Storgage => weatherPWA-step-6-1

This should have a list of all files we listed in service-worker.js

* Cache depends on updating the cache key for every change.
* Requires everything to be redownloaded for every change.

Use [sw-precache](https://github.com/GoogleChromeLabs/sw-precache) to have fine control over what gets expired, ensures requests go directly to the network and handles all of the hard work for you.

## Use service workers to cache the forecast data

Cache-first-then-network means we need to kick off two asynchronous requests, one to the cache and one to the network.

## Support native integration

### Declare an app manifest with a `manifest.json` file.

Create a `manifest.json` file in the root folder.

and in the `index.html` header include:

```html
<link rel="manifest" href="/manifest.json">
```

### Best practices:

* Place the manifest link on all your site's pages.
* The `short_name` is preferred on Chrome.
* Define icon sets for different density screens. (48dp)
* Include an icon with a size that is sensible for a splash screen and don't forget to set the `background_color`.
