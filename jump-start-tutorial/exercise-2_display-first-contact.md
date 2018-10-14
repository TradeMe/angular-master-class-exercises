# Exercise: Display first contact

Time to display our first contact! We know that component properties can be used as expressions in a component's template to display their value. In this exercise we're going to learn how to display data structures from a component, using expressions and interpolations.

![j3](https://user-images.githubusercontent.com/210413/46899525-f7d1e100-cef0-11e8-8dc2-0053d433834f.png)

## Scenario

"Hello World" is not enough. We want to build a contacts app, so eventually we're going to display a list of contacts. But let's do it one step at a time. In `src/app/models/contact.ts` you can find an interface definition of `Contact`.

Import this type and create a `contact` property of this type in `ContactsAppComponent` to render the data of a first contact in the component's template (you can find the data in the task list).

## Tasks

1. Import `Contact` from `src/app/models/contact.ts`.
2. Create a `contact` property of type `Contact` with the following object:

  ```ts
  {
    id: 6,
    name: 'Diana Ellis',
    email: '',
    phone: '',
    birthday: '',
    website: '',
    image: 'assets/images/6.jpg',
    address: {
      street: '6554 park lane',
      zip: '43378',
      city: 'Rush',
      country: 'United States'
    }
  }
  ```

3. Render the `contact` information using expressions and interpolations with the following template, **right below the toolbar** (replace the "Hello World" part with this):

  ```html
  <mat-list>
    <mat-list-item>
      <img mat-list-avatar [src]="INSERT_IMAGE_EXPRESSION HERE" alt="Picture of INSERT_CONTACT_NAME">
      <h3 mat-line>INSERT_CONTACT_NAME</h3>
    </mat-list-item>
  </mat-list>
  ```

You're probably noticing the brackets in `<img [src]="...">`. Don't be scared! If you're curious, feel free to checkout the resources for more information. We're going to talk about them later.

## Code Snippets

###### `contact.ts`

```ts
interface Address {
  street: string;
  zip: string;
  city: string;
  country: string;
}

export interface Contact {
  id: number;
  name: string;
  email: string;
  phone: string;
  birthday: string;
  website: string;
  image: string;
  address: Address;
}
```

### Additional resources and help

- [Angular's template syntax demystified](http://blog.thoughtram.io/angular/2015/08/11/angular-2-template-syntax-demystified-part-1.html)

## Next Lab

Go to [JumpStart - Lab #3](exercise-3_display-list-of-contacts.md)
