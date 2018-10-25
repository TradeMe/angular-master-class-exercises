## Exercise: Using Effects for Asynchronous Actions

In **ngrx**-land, we can use the **@Effect** decorators to solve the problems of asynchronous activity. Effects allow developers to centralize all asynchronous work. When each async activity completes then
synchronous actions are dispatched.

*  Effects should be considered **side effect** or **background processes** within an application.
*  And synchronous actions can be considered the **foreground processes**.

## Scenario

Let's use Effects for the async actions `LOAD_CONTACTS` and `UPDATE_CONTACT`. These async actions are caught by Effects. When the async work completes, the Effect will internally dispatch sync actions to update the store, e.g. `UpdateContactSuccessAction`.

> Unlike Redux, the async and sync actions [in ngrx] are still PJO(s) or class instances. The object/instances with specific action types will be directed to the Effect that has registered to listen to that action type.

Use the following diagram to refactor your application with the ngrx `@Effect()` decorator by the example of loading the list of contacts. Then apply the same concept of Effects to edit a particular contact.

![step-6-async-with-effects](https://user-images.githubusercontent.com/210413/29373606-69096ee4-8274-11e7-9d1a-3a61cd291436.jpg)

## Tasks

1. Define more ContactActions in `contacts.actions.ts`:

    *  Add two (2) more action types to `ContactsActionTypes`:

      * `LOAD_CONTACTS`, and
      * `UPDATE_CONTACT_SUCCESS`
      * We already have an `UPDATE_CONTACT` action so we don't have to create this one

    * Implement `LoadContactsAction` and `UpdateContactSuccessAction`.

    * Add both actions to `ContactsActions` to extend the union type.

2. Update `ContactsReducer` and change the action type from `UPDATE_CONTACT` to `UPDATE_CONTACT_SUCCESS` keeping the same logic.

    > Remember that we don't have to listen for `UPDATE_CONTACT` nor `LOAD_CONTACTS` because those actions will only trigger our Effects and can be seen as actions that represent async activity. Inside our reducers we only handle actions that represent synchronous activity.

3.  Create a service `ContactsEffects` with the Angular CLI and add the following imports:

    ```js
    import { Injectable } from '@angular/core';
    import { Router } from '@angular/router';
    import { Actions, Effect, ofType } from '@ngrx/effects';
    import { Observable } from 'rxjs';

    import { ContactsService } from '../../contacts.service';
    import { Contact } from '../../models/contact';

    import {
      ContactsActionTypes,
      LoadContactsSuccessAction,
      UpdateContactSuccessAction
    } from '../contacts/contacts.actions';
    ```

4. Update the constructor and inject the following dependencies to the Effect class:

    ```js
    private actions$: Actions,
    private contactsService: ContactsService,
    private router: Router
    ```

5. Implement our Effects using the `@Effect()` decorator and the action stream `actions$`.

    Implement the `getContacts$` effect:

    ```js
    @Effect() getContacts$ = this.actions$.pipe(
      ofType(ContactsActionTypes.LOAD_CONTACTS),
      switchMap(payload => this.contactsService.getContacts()),
      map((contacts: Array<Contact>) => new LoadContactsSuccessAction(contacts))
    );
    ```

    Implement the `updateContact$` effect:

    ```js
    @Effect() updateContact$ = this.actions$.pipe(
      ofType( <UPDATE_CONTACT_ACTION_TYPE> )
      map((action: UpdateContactAction) => action.payload),
      contactMap((contact: Contact) => <UPDATE_CONTACT_ON_SERVER> ),
      tap((contact: Contact) => this.router.navigate(['/contact', contact.id])),
      map((contact: Contact) => <UPDATE_CONTACT_SUCCESS_ACTION> )
    );
    ```

    * The `LOAD_CONTACTS` action is used to trigger the Effect to fetch the list of contacts from the remote database.

    * The `UPDATE_CONTACT` action triggers the Effect which will update the contact in the remote database.

6. Update `ContactsListComponent` and `ContactsEditorComponent`.

    * Remove all direct service calls to `this.contactsService.getContacts()`

    * Remove all direct service calls to `this.contactsService.updateContact(contact)`

    * Dispatch async actions, e.g. `LoadContactsAction` or `UpdateContactAction` to trigger the corresponding Effects.

7. Update `ContactsModule` in `app.module.ts` and add the following imports:

    ```js
    import { EffectsModule } from '@ngrx/effects';
    import { ContactsEffects } from './state-management/contacts/contacts.effects';
    ```

8. Add the `EffectsModule` to the imports of the `ContactsModule` and call `forRoot`.

    > This function expects an array of Effect classes as its first argument (`[ContactsEffect]`).


## Code Snippets

##### `contacts.effects.ts`

![ngrx5 1](https://user-images.githubusercontent.com/210413/47119625-14429480-d2c8-11e8-81a1-bde96de5feaa.jpg)

##### `contacts-list.component.ts`

![ngrx5 2](https://user-images.githubusercontent.com/210413/47119624-14429480-d2c8-11e8-8aeb-4dee0fd0b52d.jpg)

##### `contacts-ngrx.module.ts`

![ngrx5 3](https://user-images.githubusercontent.com/210413/47119623-14429480-d2c8-11e8-9ca2-6d7636d7ac92.jpg)


## Next Lab

Go to [Step 7: Refactor to Facade Architecture](step-6-reactor-to-facade-architecture.md)

## Technical Considerations

In our Effects above, we utilize `concatMap` to map the action payload to an inner Observable that performs an http request, e.g. `this.contactsService.getContacts()` or `this.contactsService.updateContact(contact)`. Here, it makes sense to use `contactMap` over `switchMap` because we don't want to cancel previous update requests but rather wait for them to finish before another update action is sent.

It is important to note that the **updateContact$** effect not only saves the contact it also actually routes to the contact details view. To navigate back to the details page, use the `tap` operator to perform user navigation. Notice, the **`tap`** operator only executes a callback for each event without manipulating the stream.
