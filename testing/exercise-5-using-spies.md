# Exercise: Using spies for ContactsListComponent tests

Next we want to test our `ContactsListComponent` which happens to depend on `ContactsService` as well. Since we don't want to mock all http requests in every test that might need a `ContactsService`, we want to learn how to spy on certain services to stub service responses. Let's write some tests for our `ContactsListComponent` in which we ensure, we don't make real calls to our backend.

## Tasks

1. Create a new file `src/app/contacts-list/contacts-list.component.spec.ts`
2. Create a new `describe()` block for `ContactsListComponent` and declare a fixture for it (`ComponentFixture<ContactsListComponent>`)
3. Add a `beforeEach()` block that configures a testing module using `TestBed.configureTestingModule()`
  - notice that you need `RouterTestingModule` and `ContactsMaterialModule` to satisfy DI
4. Create a fixture of `ContactsListComponent`
5. Write a test that ensures a list of contacts is fetched and rendered
  - Spy on `ContactsService.getContacts` and return a mock response
  - Perform change detection
  - Query view elements to check whether contacts are rendered
