## Lab 2: Routings Guard 

Using a Guard we can prevent navigation to happen if the Guard returns `false` or an `Observable<boolean>` which emits `false`.

## Scenario

Now that we have a split view it may easily happen that we accidentally click on another contact from the list while we have the **`ContactsEditorComponent`** open on the right hand side.

To prevent that from happening we want to implement a **`CanDeactivate`** Guard for the route to prompt the user with a question if they really like to navigate away without saving.


## Tasks

1. Create **an exported** navigation guard function `confirmNavigationGuard(component)` in `app.module.ts` which returns `window.confirm('Navigate away without saving?')`
2. Add the guard to the `canDeactivate` array of the route that shows the `ContactsEditorComponent`
3. Prevent showing the confirm dialog when the user clicks on the `Save` button

## Code Snippets

###### `app.module.ts`

![r2 1](https://user-images.githubusercontent.com/210413/46908442-4e85fc00-cf7f-11e8-9cc3-52ec8bb81cd3.jpg)

###### `app.routes.ts`

![r2 2](https://user-images.githubusercontent.com/210413/46908478-d66c0600-cf7f-11e8-9ad8-92e716b0c524.jpg)


## Next Lab

Go to [Lab #3: Navigation Gaurds](exercise-3_refactor-navigation-guard.md)
