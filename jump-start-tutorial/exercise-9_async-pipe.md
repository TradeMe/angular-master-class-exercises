# Exercise: Async Pipe

We can fine-tune our `ContactsAppComponent` a little bit further before we reached the end of this tutorial by using `AsyncPipe` in combination with our observables data structures.

## Scenario

Observable data structures can be passed directly from a component into its view and resolve by `AsyncPipe`. This makes the code a more readable since we don't have the imperative logic of resolving/subscribing to an observable. `AsyncPipe` does the job for us.

## Tasks

1. In `ContactsListComponent`, Import `Observable` from `rxjs/Observable`. 
2. Rename the `contacts` property to `contacts$` and annotate as type `Observable<Array<Contact>>`
3. Remove subscription of `contactsService.getContacts()`
4. Add `AsyncPipe` to `ngFor` expression in `ContactsListComponent`'s view

## Code Snippets


###### `contacts-list.component.ts`

![j9 1](https://user-images.githubusercontent.com/210413/46908895-eb4b9800-cf85-11e8-8590-759f42b47390.jpg)


### Additional resources and help

- [Pipes - AsyncPipe](https://angular.io/docs/ts/latest/guide/pipes.html#!#the-stateful-asyncpipe-)
- [AsyncPipe](https://angular.io/docs/ts/latest/api/common/index/AsyncPipe-class.html)
