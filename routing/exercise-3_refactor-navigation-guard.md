## Lab 3: Navigation Guards + MdDialog

In this exercise we'll learn how to create a navigation guard as a class as well as using the Angular Material `MatDialog` component to create nice and shiny dialogs.

## Scenario
Let's take our navigation guard to the next level. Right now it's just a function which returns `window.confirm()` and that's totally fine. However, instead of just showing a browser window to confirm or cancel the navigation, we want a proper dialog.

Angular Material comes with an `MatDialog` [component](https://material.angular.io/components/dialog/overview) that we can use for exactly that.

## Tasks

1. Create a file with a new navigation guard class called `CanDeactivateContactsEditorGuard`
2. Import `ContactsEditorComponent`
3. Import `CanDeactivate` from `@angular/router`
4. Create a component `ConfirmDeactivationDialogComponent` with the following template:
5. Import `MatDialogRef` from `@angular/material` and inject it into `ConformDeactivationDialogComponent` with the same generic type (Read `MatDialog`s documentation for more information)
5. Inject `dialog: MatDialog` into `CanDeactivateContactsEditorGuard`
6. Create a method `canDeactivate(component: ContactsEditorComponent)` in `CanDeactivateContactsEditorGuard` in which you call `this.dialog.open(ConfirmDeactivationDialogComponent)`
7. Return `this.dialog.afterClosed()`, which is an `Observable<boolean>`
8. Add the guard to your providers
9. In app.module, add an `entryComponents` for `ConfirmDeactivationDialogComponent`. 
10. Apply the guard to the route


## Code Snippets

###### `can-deactivate-contacts-editor.guard.ts`

![r3 1](https://user-images.githubusercontent.com/210413/46908541-d6203a80-cf80-11e8-93ed-1e3365328c49.jpg)

###### `confirm-deactivate-dialog.component.ts`

![r3 2](https://user-images.githubusercontent.com/210413/46908571-27c8c500-cf81-11e8-8801-468c56e24aa4.jpg)

###### `app.routes.ts`

![r3 3](https://user-images.githubusercontent.com/210413/46908614-d66d0580-cf81-11e8-9300-e3d0babd8829.jpg)

## Next Lab

Go to [Lab #4: Route Resolvers](exercise-4_fetch-contact-via-resolver.md)
