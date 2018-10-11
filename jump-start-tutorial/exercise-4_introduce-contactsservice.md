# Exercise: Building a service and using DI

A static list of data is just okay to try some things out or for demo purposes. However, in a real world app, we surely don't want to rely on static data, but rather have a service that takes care of providing the data we need, no matter where it comes from.

In this exercise we're going to learn how to create services and how to inject them into our application using providers.

## Scenario

`CONTACT_DATA` is an implementation detail we don't want to rely on in `ContactsAppComponent`. Create a service called `ContactsService` using angular-cli by running:

```
$ ng generate service contacts
```
Or the shorter version:
```
$ ng g s contacts
```

This will create a file in `src/app/contacts.service.ts`. Implement a method `getContacts()` that simply returns the collection of `CONTACT_DATA` for us. 

Use that new service by adding a provider to the `providers` property of the module in `app.module.ts` and injecting the service in the constructor.

Note: our app should render the same, it's just the internal architecture that has changed.


## Tasks

1. Create a `ContactsService` using angular-cli
2. Import `CONTACT_DATA`
3. Create a method `getContacts()` which returns the given data
4. Add `ContactsService` provider to the `providers` property of the module in `app.module.ts` to make the service available in your app
5. Inject `ContactsService` in `ContactsAppComponent`
6. Import `OnInit`
7. Make `ContactsAppComponent` implement `OnInit`
8. Add an `ngOnInit()` method to `ContactsAppComponent`
9. Call `ContactsService#getContacts()` to retrieve the contacts data



## Code Snippets

![j42](https://user-images.githubusercontent.com/210413/46899661-2a300e00-cef2-11e8-9079-7cad0ca5084c.jpg)


![j41](https://user-images.githubusercontent.com/210413/46899662-2ac8a480-cef2-11e8-80b9-6ef24a938707.jpg)

> Bonus: Is the `ngOnInit()` required. How could you make this code more succinct?

### Additional resources and help

- [Dependency Injection in Angular](http://blog.thoughtram.io/angular/2015/05/18/dependency-injection-in-angular-2.html)
- [Dependency Injection (angular.io)](https://angular.io/guide/dependency-injection)

## Next Lab

Go to [JumpStart - Lab #5](exercise-5_route-to-contactslistcomponent.md)

