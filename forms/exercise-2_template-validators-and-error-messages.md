## Lab 2: Template validators and error messages

In this exercise we add validation and error messages to prevent adding contacts without a name.

![f20](https://user-images.githubusercontent.com/210413/46901631-a71faf80-cf13-11e8-83f9-0e3adbd722ea.jpg)

## Scenario

We don't have any validations in our new form. Let's use the built-in `required` and `minlength` validator to have some validation and display appropriate error messages.

## Tasks

1. Add the `novalidate` HTML5 attribute to the form, so the browser's default validation is turned off
1. Disable `ContactCreatorComponent`'s save button using the forms validity state
2. Set `<mat-form-field>`'s `color` property to either "warn" or "primary" depending on if the field has errors or not
3. Add `required` and `minlength="3"` validator to the input control
4. Add an `<mat-hint>` element to into the `<mat-form-field>` if the field is not `valid` and not `pristine`. Here's a snippet:
4. Display error message inside the `<mat-hint>` element using `ngIf` for both `required` and `minlength`
5. Add information about `minlength` error in error message (`actualLength`)

## Code Snippets


###### `contacts-creator.component.html`

![f2 1](https://user-images.githubusercontent.com/210413/46991734-a0877700-d163-11e8-986d-b7816ab00356.jpg)


## Bonus Tasks

1. Refactor `ContactsEditorComponent` to also use template-driven forms and the same validation (keep in mind that one button is of type `submit` whereas the other one is of type `button`.

### Additional resources and help


## Next Lab

Go to [Forms Lab #3: Add Custom eMail Validator](exercise-3_add-custom-email-validator.md)
