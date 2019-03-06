## Exercise: Refactor to use Facade Architecture

Effects decorators are not obvious processes. Another approach to managing async activities is to use a facade class to expose the properties desired and publish methods that hide all Store and RESTful server interactions.

Since this facade class publishes properties as **Observables** we can use reactive features and the **async** pipe in our templates; and the templates will re-render when their associated observables receive emitted values.

## Scenario

Use the illustration below to guide you through the lab steps:

![lab7-using-facades](https://cloud.githubusercontent.com/assets/210413/25640329/c83ddfb2-2f54-11e7-8623-b99afd669810.jpg)

Let's implement and refactor our application to use a `ContactsFacade` class like this:

```ts
@Injectable()
export class ContactsFacade {
  // Exposed selectors
  contacts$: Observable<Array<Contact>>;
  selectedContact$: Observable<Contact>;
  loaded$: Observable<boolean>;

  constructor(
    private store: Store<ApplicationState>,
    private contactsService: ContactsService
  ) { }

  // Exposed public APIs
  getContactById(contactId: string): Observable<Contact> { ... }
  updateContact(contact: Contact): Observable<boolean> { ... }
}
```

## Tasks

1. Implement the class `ContactsFacade` in `state/contacts/contacts.facade.ts` as shown above.

    * For the Observable properties, use `this.store.pipe(select( <QUERY> ))` to initialize each property with the appropriate Observable.

    ```js
    contacts$ = this.store.pipe(select( <GET_CONTACTS_QUERY> ));
    selectedContact$ = this.store.pipe(select( <GET_SELECTED_CONTACT_QUERY> ));
    loaded$ = this.store.pipe(select( <GET_IS_LOADED_QUERY> ));
    ```


    For `getContact()`, use this as your starter code template:

    ```js
    getContactById(contactId:string):Observable<Contact> {
      // Select contact id >
      
      return this.loaded$.pipe(
        take(1),
        withLatestFrom(this.selectedContact$),   // Get latest value from selectedContact$ stream
        mergeMap(([loaded, selectedContact]) => {
          if (loaded) return Observable.of(null);

          return this.contactsService
            .getContact(contactId)
            .pipe(tap( <ADD_CONTACT_TO_LIST> ));
        }),
        // Map to contact$ stream
        mergeMap(() => this.selectedContact$)
      );
    }
    ```

    For `updateContact()`, use this as your starter code template:

    ```js
    updateContact(contact: Contact): Observable<boolean> {
      return this.contactsService
        .updateContact(contact).pipe(
            map(() => {
              <UPDATE_CONTACT_ACTION>
              return true;
            }),
            catchError(() => Observable.of(false))
        );
    }
    ```

2. Update the `ContactsModule` in `app.module.ts`:

   * Register a provider for `ContactsFacade`.

3. Update the `ContactExistGuard`, `ContactsListComponent`, `ContactsDetailComponent` and `ContactsEditorComponent` to use `ContactsFacade`.

   * Remove use of the `ContactsService`, `ApplicationState`, store, and actions

4. Update the `ContactsActions` to remove deprecated actions

   * Remove **LoadContactsAction**
   * Remove **UpdateContactAction**

## Code Snippets

##### `contacts.facade.ts`

![ngrx6 1](https://user-images.githubusercontent.com/210413/47120321-a9df2380-d2ca-11e8-9b39-07021751a215.jpg)

##### `contact-exists.guard.ts`

![ngrx6 2](https://user-images.githubusercontent.com/210413/47120320-a9df2380-d2ca-11e8-97bc-242b11b78763.jpg)


##### `contacts-list.component.ts`

![ngrx6 3](https://user-images.githubusercontent.com/210413/47120520-81a3f480-d2cb-11e8-9c01-51b3fdd42e36.jpg)


## Next Lab

Go to [Lab 7: Improve your Effects](step-7-improve-effects.md)
