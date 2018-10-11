## Exercise: Use Select and Edit Actions

The Contacts application currently uses routing and direct data-access to show
the ContactDetails and the ContactEditor views. Let's integrate our use of **ngrx**
into the workflow.

## Scenario

Let's create two (2) new actions **SelectContactAction** and **UpdateContactAction** that
will be used to view contact details or for the editor-view.

Shown below is a UML sequence diagram that clearly shows how actions will be integrated into
the workflow process. Using this diagram, make the appropriate source changes to implement this improved,
Redux workflow.

![ngrx-step-2-select-and-edit-contact](https://cloud.githubusercontent.com/assets/210413/25500318/30de6c62-2b54-11e7-8bcf-3b2d6bb6ab70.png)

## Tasks

1. Create the two (2) new actions in the `contacts-actions.ts` module.

    Implement the **SelectContactAction** class used to select the contact in the store:

    ```js
    export class SelectContactAction implements Action {
      readonly type = ContactsActionTypes.SELECT_CONTACT;
      constructor(public payload: number) { }
    }
    ```

    Implement the **UpdateContactAction** class used to save the contact changes to the server:

    ```js
    export class UpdateContactAction implements Action {
      readonly type = ContactsActionTypes.UPDATE_CONTACT;

      constructor(public payload: Contact) { }
    }

    export type ContactsActions = LoadContactsSuccessAction
      | SelectContactAction
      | UpdateContactAction;
    ```

    > Make sure to update the `ContactState` as well as the `INITIAL_STATE`.

2. Update the Contacts reducer `contacts-reducer.ts`.

    *  Using **SelectContactAction**, select the contact by the specified id (payload).
    *  Using **UpdateContactAction**, add the contact or merge the current values into appropriate contact item in the store list.

3. Modify the **ContactDetailsComponent** to use the logic shown in the UML diagram above.

4. Modify the **ContactEditorComponent** to use the logic shown in the UML diagram above.

## Next Lab

Go to [Step 3: Use Router Guard with Actions](step-3-create-contact-exists-guard.md)
