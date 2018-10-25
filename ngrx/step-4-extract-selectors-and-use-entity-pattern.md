## Exercise: Refactor with Query Selectors & Entity Pattern

Our Contacts applications has selectors defined in almost every component including `ContactsListComponent`, `ContactsDetailComponent` and `ContactsEditorComponent`. That's unfortunate because it's not really maintainable, DRY and therefore not reusable if components share common selectors.

With ngrx > 4.x we can leverage efficient selector composition using the `createSelector` function. As a result, a selector is not recomputed unless one of its arguments change. This practice is known as memoization. In addition, selectors are composable. They can be used as input to other selectors.

> A **selector** in its raw form is just a **function** that takes the application state and returns a value (e.g. contact). Used with ngrx Store, selectors are queries that return observables to values.

In addition, we want to optimize the data structure of our Store by using the Entity Pattern. This allows us to perform fast CRUD operations and simplify our reducers.

## Scenario

In this lab, we want to extract all of our selectors from the components into `contacts.reducer.ts` and compose them into a single query `ContactsQuery` to make them reusable, easier to maintain, and reduce components' responsibility. We also need to convert the Array of contacts into an entity object.

> Note: if a **store** is analogous to a database and **reducers** the tables, then **selectors** can be considered the queries into said database/store.

## Tasks

1. Change `ContactState` and refactor the `list` property to be `entities`.

    * Rename the property to `entities` and set the type to `{ [key: number]: Contact }`.
    * Don't forget to update `INITIAL_STATE`.

2. Update the `contactsReducer` so that it works with **entities** instead of an Array of contacts.

    * Specifically, you need to update `LOAD_CONTACTS_SUCCESS`, `ADD_CONTACT` and `UPDATE_CONTACT`.
    * For `LOAD_CONTACTS_SUCCESS`, make sure to flatten the Array into entities. Hint: You can use `Array.reduce`.

3. Create a `contacts.selectors.ts` file with a `namespace ContactsQuery`:

    ```js
    export namespace ContactsQuery {
      export const getLoaded = (state: ApplicationState) => state.contacts.loaded;
      ...
    }
    ```

2. Add the following queries: `getContactsEntities`, `getSelectedContactId`.

3. Use the `createFeatureSelector()` to load the NgRx state for `contacts`:

```js 
  // Lookup the 'Contacts' feature state managed by NgRx
  export const getContactsState = createFeatureSelector<ContactsState>(FEATURE_CONTACTS);
  
  export const getContactsEntities = createSelector(getContactsState, (state:ContactsState) => state.entities);
```

3. Implement the following composed queries using `createSelector`:

    * `getContacts` and
    * `getSelectedContact`

    ```js
    export const getContacts = createSelector(getContactsEntities, (entities) => {
      ...
    });

    export const getSelectedContact = createSelector(getContactsEntities, getSelectedContactId,
      (contactEntities, id) => {
        ...
      });
    ```

3. Use `ContactsQuery` selectors in `ContactsListComponent`.

4. Use `ContactsQuery` selectors in `ContactsDetailComponent`.

5. Use `ContactsQuery` selectors in `ContactsEditorComponent`. Remember to **clone** the contact **after** you selected it. You can use `map` for this.

6. Use `ContactsQuery` selectors in `ContactExistsGuard`.

## Code Snippets


###### `contacts.reducer.ts`

![ngrx4 1](https://user-images.githubusercontent.com/210413/47105965-ec403a80-d2a1-11e8-9b33-331975e9aaa1.jpg)

![ngrx4 4](https://user-images.githubusercontent.com/210413/47106765-fbc08300-d2a3-11e8-84f4-043bd5695c9e.jpg)

###### `contacts.selectors.ts`

![ngrx4 2](https://user-images.githubusercontent.com/210413/47105963-ec403a80-d2a1-11e8-862f-741b02571d96.jpg)

###### `contacts-list.component.ts`

![ngrx4 3](https://user-images.githubusercontent.com/210413/47105962-eba7a400-d2a1-11e8-8f9f-6050ac1bd373.jpg)



## Next Lab

Go to [Step 5: Apply Meta-Reducers](step-4b-apply-meta-reducers.md)
