# Exercise: Using `fakeAsync()` and `tick()`

Next we want to take a look at scenarios where components depend on router APIs that require us to simulate and asynchronous environment. Angular provides a function `fakeAsync()` that lets us write asynchronous code in a synchronous fashion. In addition, it lets us control the flow.

## Scenario

Our `ContactsDetailViewComponent` is the gateway to two different views: the contacts list and the contacts editor. In this lab we want to explore how to write tests that perform router navigation to those components using `fakeAsync()`'s execution context.

## Tasks

1. Create a new file `src/app/contacts-detail-view.component.spec.ts`
2. Create testing module in a dedicated `beforeEach()` block that sets up `ContactsDetailViewComponent` and its dependencies.
  - Make sure to use `RouterTestingModule.withRoutes()` to make our module aware of available routes.
  - Create an `ActivatedRouteStub` for dependency injection that looks like this:

    ```
    let activatedRouteStub = {
      snapshot: {
        params: { id: '0' }
      }
    }
    ```
3. Create a `ContactsDetailViewComponent` fixture, a component instance of the same and save a `contactsService` instance
4. Spy on `contactsService.getContact` and return a test contact, so we don't reach out to the API server
5. Write a test that ensures that `ContactsDetailViewComponent` fetches the correct contact (`component.contact = ???`)
   - Also check whether `contactsService` has been called with the right parameters
6. Write a test that checks whether `ContactsDetailViewComponent` emits `appTitleChange` through `EventBusService`
  - Inject `EventBustService` and spy on its `emit` method
7. Write a test that ensures it navigates to the list view 
  - spy on `Router.navigate` and check whether it has been called with the right parameters after `component.navigateToList()`
8. Write a test that ensures it navigates to editor component with the correct parameters after `component.navigateToEditor(expectedContact)`
9. Write another test that checks whether the component navigates to the list correct, but this time, use `fakeAsync()` and `tick()`.
  - Check `Location.path()` for correct state after navigation
  - Tip: this needs a spy on `router.navigate` with a `callThrough()`
10. Do the same for the editor navigation
