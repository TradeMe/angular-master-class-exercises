# Exercise: Route to your first component

The time has come! Let's implement some routing features. In this exercise we're going to route to components.

## Scenario

In order to route from our contacts list to a contact detail page, the first thing we need to do is to extract the current contacts list implementation into its own component, so that `ContactsAppComponent` is just a "frame" that holds our app, consisting of multiple components, together.

We can create a new component `ContactsListComponent` using angular-cli by running:

```console
$ ng generate component contacts-list --project=amc-starter -m=app
```
Or the shorter version:

```console
$ ng g c contacts-list -m=app
```

Using the `-m`, we specify the module this component will belong to. This will make sure the component is added to the `declarations` section of this module and you don't have to do this yourself. 

Note that in most scenario's, this step is unnecesary. The angular-cli will try to find the closest module to add this component to. Since in this case it will find two modules (contacts-material and app) at the same level in the directory hierarchy, we do need to specify it.

> Bonus: which command line argument do you use to run the command in test/dry mode?


## Tasks

1. Create a component `ContactsListComponent` with the **Angular CLI** and move the current contact list logic there from `ContactsAppComponent`
2. Create `src/app/app.routes.ts`, import the `ContactsListComponent` and export an array with routes (e.g. `export const APP_ROUTES = [...]`), holding one route pointing to `ContactsListComponent`.
3. In `app.module.ts` import `RouterModule` from `@angular/router` and `APP_ROUTES` from `./app/app.routes`
4. Add `RouterModule.forRoot(APP_ROUTES)` to the `imports` array of the module
5. Add `<router-outlet>` in `ContactsAppComponent`'s view to load and render components

## Bonus Tasks

1. Figure out how to create a route that redirects to `/` when none of the configured routes are matched by the router.

## Code Snippets

###### `contacts-list.component.ts`

![j51](https://user-images.githubusercontent.com/210413/46899695-deca2f80-cef2-11e8-8c3f-f9022359bc89.jpg)


###### `app.routes.ts`

![j52](https://user-images.githubusercontent.com/210413/46899700-19cc6300-cef3-11e8-8558-1f60760b4a1a.jpg)



### Additional resources and help

- [Routing in Angular revisited](http://blog.thoughtram.io/angular/2016/06/14/routing-in-angular-2-revisited.html)
- [Router Guide](https://angular.io/guide/router)
- [RouterOutlet](https://angular.io/docs/ts/latest/api/router/index/RouterOutlet-directive.html)

## Next Lab

Go to [JumpStart - Lab #6](exercise-6_using-routeparams.md)
