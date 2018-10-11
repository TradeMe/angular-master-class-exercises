# Exercise: Two-way data binding and sending data

Combining property binding with event binding results in two-way data binding. This exercise demonstrates how `ngModel` and two-way data binding can be used to create our first simple form.

In the last exercise we've extended our `ContactsAppComponent` to fetch its data from a remote server. Now - in this exercise - we're going to explore how to SEND data using http.

## Scenario

Displaying details of a contact is nice, but we also want to be able to edit them. We want to take advantage of Angular's `ngModel` directive that implements two-way data binding to build our first form.

This form displays a `contact` but allows for editing that contact at the same time. We have to add http capabilities to our `ContactsEditorComponent`, since it has to **send** data when we update a contact.


## Tasks

1. Create a new component `ContactsEditorComponent` using the tools you already know with the following template:
2. Import `FormsModule` from `@angular/forms` and add it to the `imports` array of the application module
3. Add a new route to `APP_ROUTES` that takes `/contact/:id/edit` that points to `ContactsEditorComponent`
4. Add a button with `RouterLink` to `ContactsDetailComponent`'s view that routes to `ContactsEditorComponent` and passes `contact.id` as `id` route parameter
6. Implement a `ContactsService` method `updateContact(contact: Contact)`, that uses `Http.put(url, data)` to send the contact that has to be updated over the wire.

  - The endpoint is `localhost:4201/api/contacts/${id}`
  - Make sure to use `PUT` method

7. In ContactsEditorComponent, inject `ContactsService`, `ActivatedRoute` and `Router` into `ContactsEditorComponent`
8. Create a `contact` property and Use `ContactsService#getContact()` in `ngOnInit()` to fetch the contact object.
9. Make sure to initialize `contact: Contact = <Contact>{ address: {}};` in `ContactsEditorComponent` since the safe navigation operator can't be used with `ngModel`
10. Render `contact` properties using `ngModel` in `ContactsEditorComponent`'s view
11. Implement a method `cancel(contact: Contact)` in `ContactsEditorComponent` that navigates to `ContactsDetailComponent` of the given contact using `Router#navigate()` (takes a routerLink dsl configuration)
12. Implement a method `save(contact: Contact)` in `ContactsEditorComponent` that uses`ContactsService#updateContact` and navigates back to `ContactsDetailComponent` as soon as the `PUT` request was successful.

## Code Snippets


###### `contacts.service.ts`

![j8 1](https://user-images.githubusercontent.com/210413/46908879-a6276600-cf85-11e8-9f6d-38f6cd59f5cb.jpg)

###### `contacts-editor.component.ts`

![j8 2](https://user-images.githubusercontent.com/210413/46908878-a6276600-cf85-11e8-86d9-8766f6effef0.jpg)

###### `contacts-editor.component.html`

  ```html
  <div class="trm-contacts-editor">
    <mat-card>
      <mat-card-title-group class="fullBleed editing">
        <img mat-card-md-image [src]="INSERT_CONTACT_IMAGE">
        <mat-card-title>INSERT_CONTACT_NAME</mat-card-title>
        <mat-card-subtitle>INSERT_CONTACT_EMAIL</mat-card-subtitle>
      </mat-card-title-group>
      <mat-card-content>
        <div fxLayout="column">
          <mat-form-field fxFlex>
            <input matInput placeholder="Name" name="name">
          </mat-form-field>
          <mat-form-field fxFlex>
            <input matInput placeholder="Email" name="email">
          </mat-form-field>
          <mat-form-field fxFlex>
            <input matInput placeholder="Phone" name="phone">
          </mat-form-field>
          <mat-form-field fxFlex>
            <input matInput placeholder="Website" name="website">
          </mat-form-field>
          <mat-form-field fxFlex>
            <input matInput placeholder="Birthday" name="birthday" type="date">
          </mat-form-field>
          <fieldset fxLayout="column">
            <legend>Address</legend>
            <mat-form-field fxFlex>
              <input matInput placeholder="Street" name="street">
            </mat-form-field>
            <mat-form-field fxFlex>
              <input matInput placeholder="Zip" name="zip">
            </mat-form-field>
            <mat-form-field fxFlex>
              <input matInput placeholder="City" name="city">
            </mat-form-field>
          </fieldset>
        </div>
      </mat-card-content>
      <mat-card-actions fxLayout fxLayoutAlign="center center">
        <button mat-button (click)="save(contact)" title="Save contact">Save</button>
        <button mat-button (click)="cancel(contact)" title="Cancel editing">Cancel</button>
      </mat-card-actions>
    </mat-card>
  </div>
  ```


### Additional resources and help

- [Template-driven Forms in Angular 2](http://blog.thoughtram.io/angular/2016/03/21/template-driven-forms-in-angular-2.html)
- [ngModel](https://angular.io/docs/ts/latest/api/common/index/NgModel-directive.html)
- [Router#navigate()](https://angular.io/docs/ts/latest/api/router/index/Router-class.html#!#navigate-anchor)
- [Angular 2 Developer Guide: Server Communication](https://angular.io/docs/ts/latest/guide/server-communication.html)
- [Taking advantage of Observables in Angular 2](http://blog.thoughtram.io/angular/2016/01/06/taking-advantage-of-observables-in-angular2.html)
- [Taking advantage of Observables in Angular 2 - Part 2](http://blog.thoughtram.io/angular/2016/01/07/taking-advantage-of-observables-in-angular2-pt2.html)

## Next Lab

Go to [JumpStart - Lab #9](exercise-9_async-pipe.md)
