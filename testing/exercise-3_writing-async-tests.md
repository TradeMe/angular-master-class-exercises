# Exercise: Writing asynchronous Tests

More often than not tests are executed in a synchronous matter. Sometimes however, we do need to leverage asynchronisity to test our code. Angular provides an `async()` function that we can use to test asynchronous APIs.

## Scenario

Our `ContactsService` comes with APIs that are based on Angular's `HttpClient` and therefore, performs asynchronous calls. Let's use `async()` to test some of those APIs.

## Tasks

1. Create a new file `contacts.service.spec.ts` in `src/app`.
2. Create a new `describe()` block for `ContactsService`
3. Add a `beforeEach()` block that creates a testing module using `TestBed.configureTestingModule()`
4. Create another `beforeEach()` block that injects `ContactsService` and assigns it to a global variable for reuse in specs.
5. Write a test for `ContactsService.getContacts()` inside of an `async()` context.
  - Notice how running the rest API is necessary here to make the test pass
6. Do the same for `getContact()`

