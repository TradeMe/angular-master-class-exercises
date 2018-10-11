## Lab 1:Create template-driven form

In this exercise we're going to build a template-driven form to add a new contact to our contacts list using Angular form directives.

![f1](https://user-images.githubusercontent.com/210413/46901357-79843780-cf0e-11e8-9a26-47785fd26c22.jpg)


## Scenario

We can list and edit our contacts, but we don't have a way to add new ones. That's why we want to create a new form component that enables us to do that.

    ```console
    $ ng generate component contacts-creator
    ```
    or

    ```console
    $ ng g c contacts-creator
    ```
    
## Tasks

1. Create a new component **ContactsCreatorComponent** using angular-cli
2. Render a form to add a new contact using the following HTML:
3. Add a new route configuration that loads `ContactCreatorComponent` with the path `contact/new` (**keep in mind that it has to be defined before `contact/:id` route**)
4. Append the following HTML to the `ContactsList` template, to create a button that links to `ContactCreatorComponent`:

  ```html
  <a routerLink="/contact/new" mat-fab title="Add a new contact" class="trm-floating-button">
    <mat-icon class="md-24">add</mat-icon>
  </a>
  ```

5. Add a new method `addContact(contact: Contact)` to **ContactsService** that performs and http POST request to `http://localhost:4201/api/contacts` with a new contact data object that is passed to this method (you can use `updateContact()` as inspiration).
6. Add `ngModel` and `ngModelGroup` to **ContactCreatorComponent**s template accordingly to submit an Contact object structure on save.
7. Get an `ngForm` reference in the template and use it's value property to submit data on save (`(ngSubmit)="save(form.value)"`).
8. Add a new method `save(contact:Contact)` to  **ContactCreatorComponent** that calls `ContactsService#addContact()` with the given contact, and navigates to **ContactsListComponent**, once the method returns.


> Note: if the `save(contact)` generates a server 404 response, ensure that the contact data submitted to the server is valid.

## Code Snippets


###### `contacts-creator.component.html`

```html
<div class="trm-contacts-creator">
  <form>
    <mat-card>
      <mat-card-title-group>
        <img mat-card-md-image alt="Placeholder image" src="/assets/images/placeholder.png">
        <mat-card-title></mat-card-title>
        <mat-card-subtitle></mat-card-subtitle>
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
            <input matInput placeholder="Birthday" name="birthday" type="date">
          </mat-form-field>
          <mat-form-field fxFlex>
            <input matInput placeholder="Phone" name="phone">
          </mat-form-field>
          <mat-form-field fxFlex>
            <input matInput placeholder="Website" name="website">
          </mat-form-field>
          <mat-radio-group name="gender">
            <mat-radio-button>
              INSERT_GENDER_VARIANT
            </mat-radio-button>
          </mat-radio-group>
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
            <mat-select placeholder="Country" name="country">
              <mat-option>INSER_COUNTRY_NAME</mat-option>
            </mat-select>
          </fieldset>
        </div>
      </mat-card-content>
      <mat-card-actions fxLayout fxLayoutAlign="center center">
        <button mat-button type="submit">Save</button>
        <a mat-button title="Cancel creating new contact">Cancel</a>
      </mat-card-actions>
    </mat-card>
  </form>
</div>  
```
  

###### `contact.ts`

```ts
export interface Contact {
  id: number | string;
  name?: string;
  email?: string;
  phone?: string | string[];
  birthday?: string;
  website?: string;
  image?: string;
  address?: Address;
}
```

###### `contacts-service.ts`

![](https://user-images.githubusercontent.com/210413/46901396-98cf9480-cf0f-11e8-8862-177631e9ee8a.png)
  
### Additional resources and help

- [Template-driven Forms in Angular](http://blog.thoughtram.io/angular/2016/03/21/template-driven-forms-in-angular-2.html)


## Next Lab

Go to [Forms Lab #2: Template Validators & Error Messages](/exercise-2_template-validators-and-error-messages.md)
