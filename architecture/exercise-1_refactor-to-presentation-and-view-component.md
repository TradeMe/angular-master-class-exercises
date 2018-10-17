## Lab 1: Refactor Details to presentation and view components

So far, all the components we've built are what's often referred to as *Business Components* or *Smart Components*. "Smart" in the sense that they know a lot about their environment. They consume business services depend on routing and more.

There's nothing wrong about this category of components. However, these components are often not really reusable. What if we would like to display contact details somewhere else in our app? Maybe embedded in another view with a different URL? That's not possible with it's current design.

In this exercise we want to learn how to refactor our *component* into:

- a *Presentation Component* that strictly communicates via inputs and outputs
- a *View Component* that embeds and controls the *Presentation Component*

![architecture-step-1](https://cloud.githubusercontent.com/assets/210413/17628008/01b38be4-6079-11e6-8083-14f678cd0541.png)

## Scenario

Let's refactor our `ContactsDetailComponent` into two components:
* a `ContactsDetailComponent` is dumb presentation view; *dumb* in the sense that it doesn't know about any routing concerns or the `ContactsService`
* a `ContactsDetailViewComponent` is the view component which does know about the `ContactsService` and `RouteParams` but doesn't know how to display a contact.

By separating these two concerns (reusable renderer and specific view component) we get to an application architecture that embraces reusability with only a slight increase in complexity.

  ```
  $ ng generate component contacts-detail-view -m app # or ng g c contacts-detail-view -m app
  ```
> The `-m app` is a long-hand version for `--module app.module.ts`. That said, if you stick to the convention of naming your module files `<name-of-module>.module.ts`. If you deviate from this naming convention you have to specify the entire filename, e.g. if you name your module file `app.feature.module.ts` you would have to pass the entire filename to the Angular CLI command: `ng g c contacts-detail-view -m app.feature.module.ts`.

## Tasks


2. Create the `navigateToEditor` and `navigateToList` methods which use the `router#navigate(dsl)` API to route to different Components; note that these are methods of the `ContactsDetailViewComponent` class.
3. Refactor the `ContactDetailComponent` to a *Presentation* component:
  1. Move the code that handles the `RouteParams` from the `ContactDetailsComponent` to the `ContactsDetailViewComponent` and expose the contact as a `contact` property
  2. Remove all routing concerns from the `ContactDetailComponent`
  3. Import `EventEmitter` and `Output` into the `ContactDetailComponent` and emit `edit` and `back` events for the button clicks
  4. Import `Input` and decorate the `contact` property as such
  5. Keep in mind that the buttons in the template are no longer anchors with links, but buttons with click handlers

## Code Snippets


###### `contacts-details-view.component.ts`

![a1](https://user-images.githubusercontent.com/210413/46903486-1a381e80-cf32-11e8-9139-9c09a534b96e.jpg)


###### `contacts-detail.component.ts`

![a2](https://user-images.githubusercontent.com/210413/46903485-199f8800-cf32-11e8-92b7-d28c28644a45.jpg)

### Web and App Servers

To launch your web application, use a Terminal session with the command  **`ng serve`**. This starts a web server for the Angular 2 application at url `http://localhost:4200`.

And since your Angular application requests data from `http://localhost:4201/api`, you will need a local server to respond to the REST API calls. Start a second, separate Terminal session with the commend: **`npm run rest-api`**.

> Note that most likely these sessions are already running... from previous exercises.


### Additional resources and help

- [Presentation vs Business vs View components](https://youtu.be/AMwjDibFxno?list=PLOETEcp3DkCq788xapkP_OU-78jhTf68j&t=247)
- [Output](https://angular.io/docs/ts/latest/cookbook/component-communication.html#!#child-to-parent)
- [Input](https://angular.io/docs/ts/latest/cookbook/component-communication.html#!#parent-to-child)


## Next Lab

Go to [Lab #2: Parent Injection into Children](exercise-2_build-tabs-using-parent-injection.md)

