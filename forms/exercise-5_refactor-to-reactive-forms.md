## Lab 5: Refactor to model-driven forms

Template-driven forms are nice and get us going very quickly. However, they are hard to test without e2e tests. In this exercise we're going to refactor our existing form to a model-driven form using `FormControl`, `FormGroup` and `FormBuilder` APIs.

## Tasks

1. Add `ReactiveFormsModule` to our application module's imports
2. Export `validateEmail()` from `src/app/email-validator.ts`
3. Export `checkEmailAvailability(contactsService)` from `src/app/email-availability-validator.ts`
4. Import `FormControl`, `FormGroup`, `FormBuilder` and `Validators` from `@angular/forms` in `ContactsCreatorComponent`
5. Import `checkEmailAvailability` and `validateEmail` functions in `ContactsCreatorComponent`
6. Inject `FormBuilder` into `ContactsCreatorComponent`
7. Create a `FormGroup` using `FormBuilder` for all fields in the form and assign it to a `form` property on the component
8. Apply validators to form fields imperatively
8. Use `[formGroup]` to associate `form` with the DOM and remove `#form="ngForm"` 
9. Use `formControlName` to associate single form controls to the input DOM elements
10. Use `form.get('FIELDNAME')` APIs to access validity state of fields and display error messages
11. Remove all validation directives from input fields in the template

## Code Snippets


###### `contacts-creator.component.ts`

![fr1 1](https://user-images.githubusercontent.com/210413/47047476-2bb04d80-d1f4-11e8-8f86-b02e0ce6414a.jpg)

###### `contact-creator.component.html`

![f43](https://user-images.githubusercontent.com/210413/46901783-64aba200-cf16-11e8-863f-6bddaee00de8.jpg)

## Bonus Tasks

1. Try to apply reactive form APIs to `ContactsEditorComponent` as well

## Next Lab

Go to [Forms Lab #6: Use form array for dynamic form fields](exercise-6_use-form-array-for-dynamic-form-fields.md)
