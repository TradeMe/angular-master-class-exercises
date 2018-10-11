# Exercise: Accessing Route Parameters

Next up, we want to route to a contact detail page.
In this exercise we're going to create a new component that is able to retrieve routing parameters.

## Scenario

The contacts app should be extended with a contact detail page. We need several things to get there:

- a new route configuration
- a new method to access a single contact in our service
- a new detail component
- we need to be able to link to that new component and pass some parameters


## Tasks

1. Create a new method `ContactsService::getContact(id: string)` which takes an id and returns a contact by that id. (Hint: you can use [`Array#find(fn)`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/find) 
  > e.g. `this.contacts.find(contact => contact.id.toString() === id);`)
2. Create a new component `ContactsDetailComponent`, using the tools you already know, with the following template:
3. Add a new route to `APPROUTES` with the path `contacts/:id` that points to `ContactsDetailComponent`
4. Change the `<mat-list-item>` in `ContactsListComponent`'s view to `<a mat-list-item>` and use the `RouterLink` directive with a DSL configuration that points to `ContactsDetailComponent`
5. Import and inject `ActivatedRoute` and `ContactsService` in `ContactsDetailComponent`
6. Create a `contact` property in `ContactsDetailComponent` and use `ActivatedRoute` and `ContactsService` to retrieve the requested contact
7. Render correct `contact` properties in `ContactsDetailComponent`'s view
8. Add `RouterLink` to get back to `ContactsListComponent`

## Code Snippets

###### `contacts.service.ts`
![](https://user-images.githubusercontent.com/210413/46899762-ee964380-cef3-11e8-91ee-d178ecd46a7a.png)

###### `contact-details.component.html`

  ```html
  <div class="trm-contacts-detail">
    <mat-card>
      <mat-card-title-group class="fullBleed">
        <img mat-card-md-image [src]="INSERT_CONTACT_IMAGE">
        <mat-card-title>INSERT_CONTACT_NAME</mat-card-title>
        <mat-card-subtitle>INSERT_CONTACT_EMAIL</mat-card-subtitle>
      </mat-card-title-group>
      <mat-card-content>
        <dl>
          <dt>Phone:</dt>
          <dd>INSERT_CONTACT_PHONE</dd>
          <dt>Website:</dt>
          <dd>INSERT_CONTACT_WEBSITE</dd>
          <dt>Birthday:</dt>
          <dd>INSERT_CONTACT_BIRTHDAY</dd>
          <dt>Street:</dt>
          <dd>INSERT_CONTACT_STREET</dd>
          <dt>Zip:</dt>
          <dd>INSERT_CONTACT_ZIP</dd>
          <dt>City:</dt>
          <dd>INSERT_CONTACT_CITY</dd>
        </dl>
      </mat-card-content>
      <mat-card-actions fxLayout fxLayoutAlign="center center">
        <a mat-button title="Go back to list">Go Back</a>
      </mat-card-actions>
    </mat-card>
  </div>
  ```
  <br/>
  
###### `contact-details.component.ts`

![](https://user-images.githubusercontent.com/210413/46899761-edfdad00-cef3-11e8-94f3-78004c57632f.png)

### Additional resources and help

- See Angular Router API: [ActivatedRoute](https://angular.io/docs/ts/latest/api/router/index/ActivatedRoute-interface.html)

## Next Lab

Go to [JumpStart - Lab #7](exercise-7_fetching-data-using-http.md)
