# Exercise: Using Directives

We learned how to bootstrap an Angular component. Let's take it one step further and explore how we can use **other** components inside our `ContactsAppComponent`.

## Scenario

Our `ContactsAppComponent` needs a nice header because, well... that's what fancy apps do, right?

The `ContactsModule` already imports the `ContactsMaterialModule`, which provides rich UI components that implement Google's Material Design specification.
Let's use the `MatToolbar` component to create our header. `ContactsMaterialModule` takes care of making that component available to us.
All we need to do is to use the component in our component's template.

## Tasks

1. Change `ContactsAppComponent`'s template to use Angular Material's `<mat-toolbar>` component. Here's a snippet:

  ```html
  <mat-toolbar color="primary">Contacts</mat-toolbar>
  ```

### Additional resources and help

- [Material Toolbar Component Docs](https://material.angular.io/components/toolbar/overview)


## Next Lab

Go to [JumpStart - Lab #2](exercise-2_display-first-contact.md)
