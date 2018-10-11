## Lab 4: Route Resolvers

We often want to postpone the activation of a route until some data is loaded. We can do exactly that using a Resolver.

## Scenario

Currently our **`ContactsDetail(View)Component`** and **`ContactsEditorComponent`** are rendered before the contact is actually loaded. In fact the loading of the contact is initiated by these components.

> Let's rewrite our application so that these components are not actually loaded until the contact was fetched successfully.


## Tasks

1. Create a file `app/shared/contacts.resolver.ts`

  1.  Create a class **`ContactsResolver`** that implements the `Resolve` interface from `@angular/router`
  2.  In the `resolve` method use the `ActivatedRouteSnapshot` and the **`ContactsService`** to fetch the contact and return the Observable
  
2. Specify a provider for the **`ContactsResolver`** in the `ContactsModule`.
3. Change the routes for **`ContactsDetail(View)Component`** and `ContactsEditorComponent` to use the **`ContactsResolver`**
4. Remove the **`ContactsService`** from `ContactsDetail(View)Component` and use `this.route.data` instead to access the contact
5. Remove all occurrences of the safe navigation operator ( `?.`) and the empty contact in both components since they aren't needed anymore.
 ```js
    contact: Contact = <Contact>{ address: {}};
````


## Code Snippets

###### `shared/contact.resolver.ts`

![r4 1](https://user-images.githubusercontent.com/210413/46908651-67dc7780-cf82-11e8-829c-0412b9977286.jpg)

## Next Lab

Go to [Lab #4: Lazy Loading Modules](exercise-5_loading-modules-asynchronously.md)
