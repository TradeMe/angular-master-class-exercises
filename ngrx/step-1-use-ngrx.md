## Exercise: Use ngrx within Contacts App

Let's use **ngrx** to configure our Contacts application to use the the core building blocks from the Redux pattern - store, reducers, and actions.

<br/>&nbsp;
![ngrx1](https://cloud.githubusercontent.com/assets/210413/25412573/3e062c2a-29e9-11e7-8371-efde3f05bf71.jpg)

## Scenario

After installing and configuring the **ngrx** library, which you don't have to do yourself as everything is already pre-installed if you followed the preparation guide, we will configure our `ContactsListView` to dispatch an **action** after the contacts list has been loaded:

![ngrx2](https://cloud.githubusercontent.com/assets/210413/25412574/3f4d8402-29e9-11e7-9221-7eb190b7e19c.jpg)

## Tasks

1.  Create the initial `src/app/state/contacts/contacts.actions.ts` module.
  * Implement the **ContactsActionTypes** and the associated **LoadContactsSuccessAction** class:
2.  Create the Contacts reducer `src/app/state/contacts/contacts.reducer.ts` to process our Contacts actions.
  * Define the `FEATURE_KEY = 'contacts'` to be used to register the reducer (in Step 6 below).
  * Define the initial state
  * Define the **contactsReducer** as a **pure** function:
4.  Update the `src/app/contacts-ngrx.module.ts` to use `StoreModule.forFeature()` register the `contacts` state management within our application by using the `StoreModule.forFeature()` function.
5.  Modify the **ContactsListComponent**:
  * Inject our custom store dispatcher.
  * Within `ngOnInit()`, use the store to query for a contacts list observable: `Observable<Array<Contact>>`. 
    > Remember to use the `select` operator from `@ngrx/store`.
  * Update `ngOnInit()` to dispatch a **LoadContactsSuccessAction** after the REST server responds with the contacts.

## Considerations

Currently the view dispatches the contact list (via an action) and the store emits that same list via our observable. 

At first glance this looks overly complex when we could simply update our `this.contacts` property directly. In subsequent labs we will continue with our ngrx integration and refactor these views several times... and you will see the benefits.

## Code Snippets

###### `contacts.actions.ts`

![ng1 1](https://user-images.githubusercontent.com/210413/46913044-1fed3d00-cfe2-11e8-8982-9cd235aa28c7.jpg)

###### `contacts.reducer.ts`

![ng1 2](https://user-images.githubusercontent.com/210413/46913187-e1a54d00-cfe4-11e8-9d12-fb9e5415f42b.jpg)

###### `contacts-list.component.ts`

![ng1 3](https://user-images.githubusercontent.com/210413/46913042-1f54a680-cfe2-11e8-9fc2-ade94c24b100.jpg)


###### `contacts-ngrx.module.ts`

![ng1 4](https://user-images.githubusercontent.com/210413/46913207-35b03180-cfe5-11e8-9468-670e640a3947.jpg)


## Next Lab

Go to [Step 2: Select and Edit Actions](step-2-select-and-edit.md)
