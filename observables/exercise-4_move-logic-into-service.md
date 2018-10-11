# Bonus Exercise: Move search logic into service

We covered all important cases of our instant search. But wouldn't it be nice if we could just hide all these details of debouncing, deduplicating and out of order responses behind a service?

Why not make our service smarter so that create a search method that has the following signature:

```ts
search(terms: Observable<string>, debounceMs = 400) : Observable<Array<Contact>>
```

>  <u>Question</u>: Why do this?<br/> 
>  The `search` method of our service takes a raw stream of terms and an optional number of ms for the debouncing and returns an `Observable<Array<Contact>>`... hiding all the complexity of the task so that it doesn't bleed into our `ContactsListComponent`.

## Scenario

In `src/app/contacts.service.ts` make a smarter `search` method that hides the complexity of debouncing, deduplicating and out of order responses from the component that uses the service.

## Tasks

1. Rename the `search` method in the `ContactsService` to `rawSearch`
2. Move the operators needed in `ContactsService` over to `contacts.service.ts` from `ContactsListComponent`
3. Build a smarter `search` method on top of `rawSearch`that hides the complexity of debouncing, deduplicating and out of order responses from its user
4. Change the `ContactsListComponent` to use the new `ContactsService#search` API

 
## Code Snippets

###### `contacts.service.ts` 
 
 ![](https://user-images.githubusercontent.com/210413/46900204-08875480-cefb-11e8-9bdb-a64eda9407b5.png)

###### `contacts-list.component.ts` 

![](https://user-images.githubusercontent.com/210413/46900224-408e9780-cefb-11e8-85e2-5c47f1a9a255.png)

 