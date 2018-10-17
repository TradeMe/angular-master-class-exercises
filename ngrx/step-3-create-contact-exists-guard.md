## Exercise: Create ContactExistsGuard

Our contacts application has an issue with deep-linking (aka bookmarking). Currently, our logic requires the list of contacts to be loaded when **navigating** to the details page. In fact, `ContactsDetailComponent` retrieves the selected contact to show its details in the HTML template of the component.

One way to fix this problem is to implement a router guard which will "protect" a specific part of our application. Guards can re-route and multiple guards can protect a single route.

With a router guard we can make sure that the contact is loaded before we navigate and show the contact's details. Note that in contrast to `ContactsListComponent` were we would fetch all contacts, `ContactsDetailComponent` loads one (1) specific contact.

> You might wonder why we are using a guard instead of a resolver. The reason being is that we are not interested in the data returned by a resolver because all of our application state is stored in a single immutable state tree (Store). As such a **guard** makes more sense for this scenario.

## Scenario

Let's refactor our contacts application and allow deep linking by implementing a `ContactExistsGuard`. Use the UML sequence diagram below to help with your code challenge in this lab:

![ngrx_contactdetail_router_guard](https://cloud.githubusercontent.com/assets/210413/25588493/21679b24-2e6e-11e7-8072-58bce451f333.png)

## Tasks

1. Create a new action type for `ADD_CONTACT` and add it to the `ContactsActionTypes` in `contacts.actions.ts`.

2. Implement `AddContactAction` and use the previously created action type.

    * Make sure the payload of the action class is of type `Contact`.

    * Don't forget to add `AddContactAction` to the union type `ContactsActions` that is used inside the `ContactsReducer`.

3. Update `contacts-reducer.ts` to handle storing a single contact using the action type `ADD_CONTACT`:

   * First, check whether the contact is in the list. Tip: You can use `Array.find`.  

   * If the contact is already in the list, do nothing and return a new array containing all contacts.

   * If the contact was not found, extend the list of contacts and add the new contact to the list.
   Tip: You can use the spread operator for array literals. Example: `[...myCollection, myItem]`.
   This creates a new list with all the items from `myCollection` plus an additional item `myItem`. If the contact was found, we don't have to do anything and we can return the list unmodified.

   * Add a new property `loaded` to the `ContactState` interface. This is used to determine if the list was already loaded. The type will be `boolean` and the inital value should be `false`. Set this property to `true` when `LoadContactsSuccessAction` was dispatched.

4. Create a `ContactExistsGuard` in `/src/app/contact-exists.guard.ts` and implement the `CanActivate` interface. You can do that using the Angular CLI: `ng g g contact-exists -m app`:

    * In the `canActivate()` method, dispatch `SelectContactAction` and give it the contact id from the `ActivatedRouteSnapshot` using `route.paramMap.get('id')`.

    * Select `loaded` from the store in order to check whether the list was already fetched. Make sure to
      chain `take(1)` to your stream which returns a specified number of contiguous events. In this case
      we are only interested in the `loaded` property **once**.

      > Remember that `store.pipe(select(<function>))` returns an observable.

    * Use `switchMap` to map to an inner observable which will be the results of `this.contactsService.getContact(contactId)`.

    * If you are calling `getContact` make sure to dispatch `AddContactAction` once the http call has been resolved.

    *  Map the inner observable to a boolean using `.map(contact => !!contact)`.

        > This is necessary because the `canActivate` functions returns either a boolean, `Promise<boolean>`
        > or `Observable<boolean>`.

5. Add `ContactExistsGuard` provider to the `providers` array of the `ContactsModule` in `app.module.ts` to make the guard available in your app. If you used the Angular CLI this should have been taken care of already. Though, it's better to verify this one more time to be safe.

6. Update the route configuration.

    * Add the guard to the `canActivate` array of the routes that show the `ContactsDetailComponent` and
    `ContactsEditorComponent`.

7. Update both `ContactsDetailComponent` and `ContactsEditorComponent` so that they don't dispatch
   the `SelectContactAction` anymore.

    > This is now handled by the guard.


## Code Snippets

###### `/src/app/contact-exists.guard.ts`

![ngrxl3 1](https://user-images.githubusercontent.com/210413/47104576-43441080-d29e-11e8-936c-e121ed1c850a.jpg)

## Next Lab

Go to [Step 4: Extract Selectors](step-4-extract-selectors-and-use-entity-pattern.md)
