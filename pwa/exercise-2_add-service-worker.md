# Exercise: Add a Service Worker

In order to become a true PWA, our app has to work offline as well! Service Workers have been designed for exactly that as they offer APIs to control where requests go and what is going to be returned from them, as well as caching.

## Scenario

In the next step we want to add Angular's Service Worker to our application and make it cache any kind of static assets and resources so that parts of our app will work offline.

## Tasks

1. Active Service Worker support in your CLI project by adding `serviceWorker: true` to `angular.json`
2. Import `ServiceWorkerModule` from `@angular/service-worker` in `app.module.ts` and make it `register()` the `/ngsw-worker.js`. Ensure it's only enabled in production mode
3. Create an `ngsw-config.json` in `src`
4. Add two `assetGroups` objects, one named `app` with a `prefetch` installation mode, and one named `assets` with a `lazy` installation mode
5. Add files, urls, resources, accordingly to cache static resources and assets.

### Additional resources and help

- [Angular Service Worker Intro](https://angular.io/guide/service-worker-intro)

