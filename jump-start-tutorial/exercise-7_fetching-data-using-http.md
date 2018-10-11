# Exercise: Fetching data using Http

In this exercise we're going to replace our static `CONTACT_DATA` with actual http requests to fetch the data from a remote web server.

## Scenario

Until now we've worked with static (mock) data provided by collection via our `ContactsService`. We now want to take it one step further and fetch this data from a server using Angular's `Http` layer.

In order to make http work, we need to configure our application's dependency injector and teach it some http capabilities. Just like for the router, Angular provides a module `HttpClientModule` that we have to import from `@angular/common/http`.

We also need to import operators for the Reactive Extensions. In this exercise we're mainly interested in the `map()` function which we can import from `rxjs/operators`. We will use these new tools to extend `ContactsService` to use `Http` and fetch the contacts data from `http://localhost:4201/api`. 


## Tasks

1. Run `npm run rest-api` from another terminal session to start the REST API server
2. Import `HttpClientModule` from `@angular/common/http` and add it to the `imports` array of our module
3. Import `map` from `rxjs/operators` in `src/app/contacts.service.ts`
4. Import `HttpClient` and inject it into `ContactsService`
5. Create a property `API_ENDPOINT` with the value of `http://localhost:4201` in `ContactsService`
6. Change `getContacts()` so that it uses `Http.get()` to fetch contacts data from `http://localhost:4201/api/contacts`.
7. Do the same for `getContact()`. Keep in mind that this API expects a parameter (`http://localhost:4201/api/contacts/${id}`
8. Change `ContactsService` usage in `ContactsDetailComponent` and `ContactsListComponent` since it's now based on observables
9. Fix rendering in `ContactsDetailComponent`'s view using safe navigation operator (`contact?.[PROPERTY]`)

## Bonus Tasks

1. You might notice that the image in `ContactsDetailComponent` cause `404` errors. Can you find a solution for it?
2. Currently the api endpoint is hard-coded right into `ContactsService`. Can you find a way to make it injectable throughout your application? Give it a try!

  (hint: we need **string token** e.g. "API_ENDPOINT" and a new decorator called `@Inject`)

2. Because "API_ENDPOINT" is a very generic name, we want to make sure to not run into naming collisions. Find out how you can use `InjectionToken` and refactor the previous implementation.

## Code Snippets

###### `contacts.service.ts`

![j7 1](https://user-images.githubusercontent.com/210413/46908823-11bd0380-cf85-11e8-89c2-0863225f4b38.jpg)


###### `contacts-detail.component.ts`

![j7 2](https://user-images.githubusercontent.com/210413/46908822-11bd0380-cf85-11e8-8b83-ae3fe4ab3863.jpg)

### Additional resources and help

- [Taking advantage of Observables in Angular](http://blog.thoughtram.io/angular/2016/01/06/taking-advantage-of-observables-in-angular2.html)
- [Taking advantage of Observables in Angular - Part 2](http://blog.thoughtram.io/angular/2016/01/07/taking-advantage-of-observables-in-angular2-pt2.html)
- [Understanding OpaqueToken in Angular](http://blog.thoughtram.io/angular/2016/05/23/opaque-tokens-in-angular-2.html)


## Next Lab

Go to [JumpStart - Lab #8](exercise-8_two-way-data-binding-and-sending-data.md)
