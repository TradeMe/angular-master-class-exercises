# Exercise: Use HttpTestingController

While using `async()` for asynchronous tests might be very convenient, when it comes to http calls specifically, we'd rather like to avoid reaching out to our servers every time we execute a test. That's why Angular comes with `HttpClientTestingModulde` and a `HttpClientTestingController` that we can leverage to write tests in which we control the flow of any http calls.

## Scenario

Let's refactor our current tests for `ContactsService` to use `HttpTestingModule` and explore the APIs of `HttpTestingController` to make testing http calls a breeze.

## Tasks

1. Create a new `describe()` block that comes with its own `beforeEach()`
  - make sure the `describe()` is a "sibling" of our previous `describe()` so they don't share the same context
2. Set up a new testing module using `TestBed.configureTestingModule()`, that imports `HttpTestingModule`
3. Add another `beforeEach()` block that injects and instantiates `ContactsService` and `HttpTestingController`
4. Write a test that ensures `getContacts()` returns a list of contacts
  - Create a mock response that looks like this

    ```
    cont mockResponse = {
      items: [
        { id: 0, name: 'First contact' },
        { id: 1, name: 'Second contact' }
        { id: 3, name: 'Third contact' }
      ]
    }
    ```
  - use `httpTestingController.expectOne(url)` to expect a single API call
  - Flush the ongoing request with `mockResponse` and add your expectations
  - Verify no outstanding requests using `httpTestingController.verify()`
5. Do the same for `getContact()` and `updateContact()`
