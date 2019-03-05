## Lab 3: Deal with out of order responses

Our instant search works pretty decent already but there's one thing that we haven't dealt with yet. Namely, out of order responses.

Consider the following:

The user enters *Christoph*, pauses, clears the search box, and enters *Pascal*. The application issues two search requests, one for *Christoph* and one for *Pascal*.

A load balancer could dispatch the requests to two different servers with different response times. This means, we can't be sure which of the requests will come back first or second. The results from the first *Christoph* request might arrive after the later *Pascal* results. The user will be confused if we display the *Christoph* results to the *Pascal* query.

In order to fix that problem we have to combine the Observable of terms with the Observable of API response using the `switchMap` operator. The `switchMap` will take care of unsubscribing from Observable API responses as soon as new requests are issued. By combining the input stream (what the user types) with the output stream (what the server responds) through the `switchMap` operator we get a new, more sophisticated Observable that only yields the results that we are interested in.

## Scenario

In `src/app/contacts-list/contacts-list.component.ts` in the `ngOnInit` method, combine the Observable of terms (`Observable<string>`) and the Observable of API responses (`Observable<Array<Contact>>`) by using the `switchMap` operator. Expose the new Observable to `this.contacts`. This will prevent out of order responses to mess with the UI.

There's one more catch though. So far we've used `this.contacts = this.contactsService.getContacts()` in `ngOnInit` to show the initial list of contacts. Clearly, if we just follow what we explained above we end up overwriting the value of `this.contacts` and end up with a list that's initially empty.

Fortunately we can simply use the `merge` static method to merge in `this.contactsService.getContacts()` to display the initial list of contacts.

## Tasks

1. Import `switchMap` just as we did with the other operators
2. Import `merge` from `rxjs`
3. In `ngOnInit` use `switchMap` operator to combine the stream of terms with the `search` method producing an `Observable<Array<Contact>>`
4. Merge the stream with the `Observable` returned by `this.contactsService.getContacts()` for the initial state of the list
5. Remove the obsolete `search(term: string)` method from the component

 
## Code Snippets

###### `contacts-list.component.ts` 
 
 ![](https://user-images.githubusercontent.com/210413/46900129-c27dc100-cef9-11e8-933c-6aa6b2deb067.png)
 

## Bonus Tasks

1. Simulate that the initial loading of contacts takes 5000ms (e.g. `contactsService.getContacts().pipe(delay(5000))`). 
 This causes search results to get overwritten by the full list when performing a search quickly after the application  starts. Find a way to get around this.
 >  Hint: use the `takeUntil()` operator.
 
 
## Next Lab
Go to [Observables Lab #4: Refactor to Service](exercise-4_move-logic-into-service.md)
