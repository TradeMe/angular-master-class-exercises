# Exercise: Display list of contacts

The goal of this exercise is to explore and discuss how we create lists dynamically based on data collections that derived from a component's property. Let's create a list of contacts.

![j3](https://user-images.githubusercontent.com/210413/46899611-92322480-cef1-11e8-92ae-5056f48248c7.png)


## Scenario

In order to render a list of contacts, we need data that we can actually work with. Take a look at `src/app/data/contact-data.ts`. What you'll find is a data collection of contacts.



Import that data, assign it a `contacts` property of `ContactsAppComponent` and use the `ngFor` directive to render a HTML list, based on that data, in `ContactsAppComponent`'s view.

## Tasks

1. Import `CONTACT_DATA` from `data/contact-data.ts` in ContactsAppComponent.
2. Create a property `contacts` in `ContactsAppComponent` and assign the collection.
3. Extend the existing static list in `ContactsAppComponent`'s view with `ngFor` and render a list item for each contact in the collection.

> Do not copy and paste the above code!

## Bonus Tasks

1. Figure out what `ngFor`'s `trackBy` property is about and use it to make `ngFor` track the list by the contact ids.

## Code Snippets

###### `contact-data.ts`

![js30](https://user-images.githubusercontent.com/210413/46899281-cc012c00-ceed-11e8-9c91-b8ec2ae9fe3f.png)

###### `contacts-app.component.ts`

![js3 1](https://user-images.githubusercontent.com/210413/46899218-12a25680-ceed-11e8-90cc-cffd8ba8c81c.png)


### Additional resources and help

- See the Angular API: [NgFor](https://angular.io/guide/template-syntax#ngfor)

## Next Lab

Go to [JumpStart - Lab #4](exercise-4_introduce-contactsservice.md)
