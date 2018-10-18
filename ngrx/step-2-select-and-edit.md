## Exercise: Use Select and Edit Actions

The Contacts application currently uses routing and direct data-access to show
the ContactDetails and the ContactEditor views. Let's integrate our use of **ngrx**
into the workflow.

## Scenario

Let's create two (2) new actions **SelectContactAction** and **UpdateContactAction** that
will be used to view contact details or for the editor-view.

## Tasks

1. Create the two (2) new actions in the `contacts-actions.ts` module. 
 * Implement the **SelectContactAction** class used to select the contact in the store:
 * Implement the **UpdateContactAction** class used to save the contact changes to the server:
2. Update the Contacts reducer `contacts-reducer.ts`. 
 * Using **SelectContactAction**, select the contact by the specified id (payload).
 * Using **UpdateContactAction**, add the contact or merge the current values into appropriate contact item in the store list.
3. Modify the **ContactDetailsComponent** to use the logic shown in the UML diagram above
 *  ngOnInit() should dispatch `SelectContactAction`
 *  `contact$ : Observable<Contact> = this.store.select(...)`
4. Modify the **ContactEditorComponent** to use the logic shown in the UML diagram above.
 *  ngOnInit() should dispatch `SelectContactAction`
 *  `contact$ : Observable<Contact> = this.store.select(...)`
 *  `save()` should call `ContactsService::UpdateContact()` and then dispatch `UpdateContactAction()` and then route to the contact details.
  
## UML Flow Diagrams

Shown below is a UML sequence diagram that clearly shows how actions will be integrated into
the workflow process. Using this diagram, make the appropriate source changes to implement this improved,
Redux workflow.

![ngrx-step-2-select-and-edit-contact](https://cloud.githubusercontent.com/assets/210413/25500318/30de6c62-2b54-11e7-8bcf-3b2d6bb6ab70.png)

## Code Snippets

###### `contacts.actions.ts`

```ts
export class SelectContactAction implements Action {
  readonly type = ContactsActionTypes.SELECT_CONTACT;
  constructor(public payload: number) {}
}

export class UpdateContactAction implements Action {
  readonly type = ContactsActionTypes.UPDATE_CONTACT;

  constructor(public payload: Contact) {}
}

export type ContactsActions = 
    LoadContactsSuccessAction
    | SelectContactAction
    | UpdateContactAction;
```
    
###### `contacts.reducer.ts`

![ngrx2 1](https://user-images.githubusercontent.com/210413/47127084-22a0a880-d2e8-11e8-84dd-fc71b0ab3cfe.jpg)

###### `contacts-detail.component.ts`

![ngrx2 2](https://user-images.githubusercontent.com/210413/46927554-7ca83080-d092-11e8-89a6-5580c2dda015.jpg)

###### `contacts-editor.component.ts`

![ngrx2 3](https://user-images.githubusercontent.com/210413/46927724-6cdd1c00-d093-11e8-990e-a09ad92ee999.jpg)

## Next Lab

Go to [Step 3: Use Router Guard with Actions](step-3-create-contact-exists-guard.md)
