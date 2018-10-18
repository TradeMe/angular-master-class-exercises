## Exercise: Improve Effects with Deciders/Splitters

Effects can also be used to:
  * Split 1 action into multiple actions; to spawn 1..n other actions
  * Decide on *output action(s)* based on input content or biz logic
  
## Scenario

Let's improve our `contacts.effects.ts` to improve our logic to load all contacts. Now the Effect should contain the logic to check `facade.loaded$` and decide if the all contacts should be loaded from the server or if the action should be ignored if that list was already loaded.

Let's also list for `LOAD_CONTACT_DETAILS` to BOTH (1) select the contactId and (2) load the contact details.
 

## Tasks

1. In **`contacts.actions.ts`** create 
  * a `class NoopAction` action class that does not have a payload.
  * a `class LoadContactAction` to load a contact information (used in Content-based Decider below)
  * a `class LoadContactDetailsAction` class that requests to load details of a specific contact. (used in Action Splitter below)
2. In **`contacts.effects.ts`** create an 
  * **Content-Based Action Decider** `@Effect() getContact$` that checks `facade.loaded$` to determine if the action should be ignored (and return the NoopAction) or if the contact should be loaded (using the contactsService).
  * **Action Splitter** `@Effect() getContactDetails$` that will emit 2 actions: `SelectContactAction` and `LoadContactAction` 
3. Make sure all view components are using ONLY the ContactsFacade observables and methods; remove all uses of Store and ContactsService
4. Update **`ContactsFacade::getContactById(contactId)`** to dispatch actions to use these new effects.

## Code Snippets

##### `contacts.effect.ts`

![ngrx8 1](https://user-images.githubusercontent.com/210413/47187879-44ef0080-d392-11e8-9785-20f3a7ff732b.jpg)

![ngrx8 2](https://user-images.githubusercontent.com/210413/47187878-44566a00-d392-11e8-9c9d-b1dd41ab7204.jpg)

##### `contacts.facade.ts`

![ngrx8 3](https://user-images.githubusercontent.com/210413/47188227-b7acab80-d393-11e8-9b21-9e578ed13a03.jpg)


## Next Lab

Congratulations! You are done.
