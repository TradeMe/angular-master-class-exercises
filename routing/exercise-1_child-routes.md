## Lab 1: Children Routes

Using children routes we can build components with nested `<router-outlet>`'s to implement more sophisticated
scenarios.

Currently our app always shows just one screen at a time. We like to change our application to have two main views where the first is a split view that has the list of contacts on the left and opens a contact on the right. 

![r1](https://user-images.githubusercontent.com/210413/46908247-9ce5cb80-cf7c-11e8-9864-d26a989c71b6.jpg)

## Scenario

The contacts can still be edited so the right hand side of the split view is either filled with the `ContactsDetail(View)Component`, or the `ContactsEditorComponent`. The default route will simply redirect to `contact/0`.

In terms of `<router-outlet>`'s that means that we need a `<router-outlet>` on our **`ContactsAppComponent`** component to either inject the component that assembles the split view (let's call it **`ContactsDashboardComponent`**) or the component that shows the about page.


At the same time our **`ContactsDashboardComponent`** also needs a `<router-outlet>` to toggle the right hand side between the **`ContactsDetailComponent`** and the **`ContactsEditorComponent`**.

<br/>

![master-details](https://cloud.githubusercontent.com/assets/210413/21835265/b6d82d78-d80f-11e6-938d-a486f8a11f19.png)


## Tasks

1. Create a **`ContactsDashboardComponent`** for the split view
2. Configure the routes for the **`ContactsDashboardComponent`** with the different child routes for the right hand side of the split view
3. In the **`ContactDetail(View)Component`** subscribe to `this.route.params` to retrieve the `id` instead of using the snapshot. The snapshot can't be used since the component may be reused
4. Redirect the default route to `contact/0` (`{ path: '', redirectTo: 'contact/0', pathMatch: 'full' }`)
5. Create an **`AboutComponent`** for the about page
6. Configure a route to load the **`AboutComponent`** for the `about` url
7. You may also want to remove the back button from the **`ContactDetail(View)Component`**

## Code Snippets

In order to be able to actually navigate to the about page we'll change the header in `ContactsAppComponent`'s template to this:

###### `app.component.html`

![r1 2](https://user-images.githubusercontent.com/210413/46908346-04e8e180-cf7e-11e8-8b28-508b06aa3658.jpg)


For the `ContactsDashboardComponent`, we want to use Angular Materials' `MatDrawer` component to render the `ContactsListComponent`. The template can be as simple as this.

###### `contacts-dashboard.component.html`

![r1 3](https://user-images.githubusercontent.com/210413/46908387-8cceeb80-cf7e-11e8-939f-5bbd64c1b472.jpg)


###### `contact-detail-view.component.ts`

![r1 1](https://user-images.githubusercontent.com/210413/46908310-92780180-cf7d-11e8-8261-9ecf4328a268.jpg)

###### `about.component.ts`

```html
<div class="trm-about">
  <mat-card fxLayout="column" fxFlex fxLayoutAlign="center center">
    <h2 mat-card-title>Angular Master Class</h2>
    <mat-card-content>
      <img src="/assets/images/team.jpg" alt="Team thoughtram">
      <p style="text-align: center;">Brought to you by thoughtram</p>
    </mat-card-content>
    <mat-card-actions>
      <a mat-button title="Go back to dashboard" 
         routerLink="/">
        Go Back
      </a>
    </mat-card-actions>
  </mat-card>
</div>
```

----

## Web and App Servers

To launch your web application and the REST server, use a Terminal session with the command:
  
```console
$   ./start
```

## Next Lab

Go to [Lab #2: Router CanDeactivate](exercise-2_can-deactivate.md)
