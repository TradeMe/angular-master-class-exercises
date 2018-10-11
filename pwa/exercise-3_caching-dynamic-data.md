# Exercise: Caching dynamic data

Service Workers go far beyond fetching and catching static assets. They can fetch and respond to any request, including API calls where the returned data might change over time. In this lab we'll learn how to cache dynamic data.

## Scenario

While static parts of our app are now being cached and already offer a bit of an improvement, users still won't see any contacts in case they are offline. That's because we don't cache any API responses yet. Let's fix that!

## Tasks

1. Add a `dataGroup` named `contacts-api` and make it fetch and cache responses for `/api/contacts`
2. Specify the `performance` strategy and notice how it affects the way of the service worker prioritises loading from cache first
3. Add a `dataGroup` named `contact-api` and make it fetch and cache responses for `/api/contact/*`
4. Apply the same conditions

Test whether your app works offline with dynamic data being cached!

### Additional resources and help

- [Angular Service Worker Configuration](https://angular.io/guide/service-worker-config)

