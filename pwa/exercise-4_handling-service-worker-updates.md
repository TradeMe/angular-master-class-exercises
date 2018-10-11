# Exercise: Handling Service Worker updates

Great! Our app now fully works offline. Running a progressive web app audit will show that we're scoring quite well. The only thing we don't offer right now locally is https support, but we can live with that.

## Scenario

One thing we don't handle very well yet however, is updates to our app and the service worker. Imagine we're deploying a new version of our app but the user will never receive it because the service work does its job. In this lab we'll implement an update check and notification mechanism that lets the user update the installed service worker on their device.

## Tasks

1. Add `MatSnackBarModule` to `ContactsMaterialModule`
2. Import `MatSnackBar` from `@angular/material` in `app.component.ts` and inject it into `ContactsAppComponent`.
3. Import `SwUpdate` from `@angular/service-worker` in `app.component.ts` and inject it into `ContactsAppComponent`.
4. Subscribe to `swUpdate.available` and use `snackBar.open()` to show a snackbar whenever there's a new Service Worker version available
5. Ensure the notification has a `Reload` action which uses `swUpdate.activateUpdate()` to enforce activation of the latest service worker version
6. Use then `document.location.reload()` to reload the app

You can test your updates by making changes to any assets and rebuilding the app again. Watch out that the right service worker version is installed when testing!

### Additional resources and help

- [Angular Service Worker in Production](https://angular.io/guide/service-worker-devops)

