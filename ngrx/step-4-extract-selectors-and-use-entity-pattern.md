## Exercise: Refactor Query Selectors and use Entity Pattern

Our Contacts applications has selectors defined in almost every component including `ContactsListComponent`, `ContactsDetailComponent` and `ContactsEditorComponent`. That's unfortunate because it's not really maintainable, DRY and therefore not reusable if components share common selectors.

With ngrx > 4.x we can leverage efficient selector composition using the `createSelector` function. As a result, a selector is not recomputed unless one of its arguments change. This practice is known as memoization. In addition, selectors are composable. They can be used as input to other selectors.

> A **selector** in its raw form is just a **function** that takes the application state and returns a value (e.g. contact). Used with ngrx Store, selectors are queries that return observables to values.

In addition, we want to optimize the data structure of our Store by using the Entity Pattern. This allows us to perform fast CRUD operations and simplify our reducers.

## Scenario

In this lab, we want to extract all of our selectors from the components into `contacts.reducer.ts` and compose them into a single query `ContactsQuery` to make them reusable, easier to maintain, and reduce components' responsibility. We also need to convert the Array of contacts into an entity object.

> Note: if a **store** is analogous to a database and **reducers** the tables, then **selectors** can be considered the queries into said database/store.

## Tasks

1. Change `ContactState` and refactor the list property to be entities.

    * Rename the property to `entities` and set the type to `{ [key: number]: Contact }`.
    * Don't forget to update `INITIAL_STATE`.

2. Update the `contactsReducer` so that it works with **entities** instead of an Array of contacts.

    * Specifically, you need to update `LOAD_CONTACTS_SUCCESS`, `ADD_CONTACT` and `UPDATE_CONTACT`.
    * For `LOAD_CONTACTS_SUCCESS`, make sure to flatten the Array into entities. Hint: You can use `Array.reduce`.

3. Create a `namespace` below the `contactsReducer` in `contacts.reducer.ts`:

    ```js
    export namespace ContactsQuery {
      export const getLoaded = (state: ApplicationState) => state.contacts.loaded;
      ...
    }
    ```

2. Add the following queries: `getContactsEntities`, `getSelectedContactId`.

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

## Next Lab

Go to [Step 5: Apply Meta-Reducers](step-5-apply-middleware.md)
