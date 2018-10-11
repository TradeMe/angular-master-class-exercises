## Lab 2: Debounce and deduplicate terms

The goal of this exercise is to fine-tune the existing implementation of our instant search to leverage the power of observables. We will debounce and deduplicate the user supplied search terms in order to reduce the pressure on the server and increase scalability.


![o1](https://user-images.githubusercontent.com/210413/46899916-741af300-cef6-11e8-9c24-d055e447b798.jpg)


## Scenario

In `src/app/contacts-list/contacts-list.component.ts` create a `Subject` to be used from within the template to push the search term as it changes. We need to have this term changes as an Observable so that we can use the power of the `debounce` and `distinctUntilChanged` operator to reduce the number of requests made to the server.

In `src/app/contacts-list/contacts-list.component.html` change the way the input changes are propagated so that they get pumped into the Subject that our `ContactsListComponent` now holds on to.

## Tasks

1. Create a `Subject` in `ContactsListComponent` that can be used from the template to propagate the input changes
  - Update the `(input)` event handler of the search input to call `terms$.next($event.target.value)`
  - import `Subject` from `rxjs`
  - create an instance property `terms$` and initialize it with `new Subject<string>();`
  >  Make sure to import `debounceTime` and `distinctUntilChanged` just like you did for `map`
2. Subscribe to `terms$` observable and perform `search(term)`
3. Use the `debounceTime(400)` and `distinctUntilChanged()` operator to reduce the number of requests made to the server


## Code Snippets


###### `contacts-list.component.ts`

![](https://user-images.githubusercontent.com/210413/46900071-acbbcc00-cef8-11e8-8117-44923f966775.png)

###### `constacts-list.component.html`

![](https://user-images.githubusercontent.com/210413/46900070-acbbcc00-cef8-11e8-9756-9022ef9294eb.png)



## Next Lab
Go to [Observables Lab #3: Out of Order Responses](exercise-3_deal-with-out-of-order-responses.md)
