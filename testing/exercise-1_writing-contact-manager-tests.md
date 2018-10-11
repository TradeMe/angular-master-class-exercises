# Exercise: Writing tests for ContactManager class

After we explored the basic APIs to write or first tests for our Angular application, let's get our feet wet and write some code. In this lab we'll write tests for an artificial `ContactManager` class.

## Scenario

The `ContactsManager` class located in `src/app/data/` comes with different APIs such as:

- `getAll()` - to get all contacts
- `get(id: string)` - to get a single contact
- `add(contact: Contact)` - to add a single contact
- `update(contact: Contact)` - to update a single contact

Let's write our first basic tests using the Jasmine testing library, that check whether our methods do what they need to do.

## Tasks

1. Create a new file `contacts-manager.spec.ts` in `src/app/data`.
2. Create a `describe()` block for `ContactsManager`
3. Add a `beforeEach()` block that instantiates a new instance of `ContactsManager` for each spec.
  - import `CONTACT_DATA` from `./contact-data` and use it to initialize the `ContactManager`
4. Write a test that checks whether `ContactsManager.getAll()` returns all contacts.
5. Write a test that checks whether `ContactsManager.get(id)` returns a single contact by given id.
6. Write a test that ensures `ContactsManager.get(id)` returns `null` if no contact exists for a given id.
7. Write a test that checks whether adding a new contact using `ContactsManager.add(contact: Contact)` works
  - You can read `ContactsManager.contacts` to check the existence of the added contact
8. Write a test that ensures `ContactsManager.update()` throws when the contact under update doesn't exist.
  - **Tip:** Use the `toThrowError` matcher to see if a function throws an error!
9. Write a test that ensures updating contacts works.
