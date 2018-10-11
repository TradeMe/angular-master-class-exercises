## Lab 3: Add custom email validator

## Scenario

Write your first custom validator.

The email field is optional, which is okay. However, we're able to enter whatever we want. Let's make sure the entered value is an actual email address.

![f22](https://user-images.githubusercontent.com/210413/46901606-5c059c80-cf13-11e8-9a00-f5376fc19aa1.jpg)

## Tasks

1. Create a new directive using angular-cli `ng generate directive email-validator`
2. Import `FormControl` from `@angular/forms` in that file
2. Write a stand-alone **function** `validateEmail(c: FormControl)` that uses a regular expression to test the value of the given control.
  - The Regexp is: 
  
  ```ts 
  const VALID_EMAIL = /^[a-z0-9!#$%&'*+\/=?^_`{|}~.-]+@[a-z0-9]([a-z0-9-]*[a-z0-9])?(\.[a-z0-9]([a-z0-9-]*[a-z0-9])?)*$/i;
  ```
3. Use `.test()` on the regexp to check if control value is an email address
4. In case of an error, return an object that looks like this:

  ```ts
  {
    validateEmail: {
      valid: false
    }
  }
  ```

3. Change `EmailValidator` directive's selector to `[trmValidateEmail][ngModel]`
4. Add the new validator to the `NG_VALIDATORS` multi provider
5. Add `EmailValidator` to the ngModule **`declarations`** in `app.modules.ts` (probably already one by angular cli)
6. Apply `trmValidateEmail` directive on email input control
7. Set `<mat-form-field>`'s `color` property to either "warn" or "primary" depending on if the field has errors or not
8. Add an `<mat-hint>` element to into the `<mat-form-field>` if the field is not `valid` and not `pristine`. Here's a snippet:

## Code Snippets

###### `email-validator.directive.ts`

![group 10](https://user-images.githubusercontent.com/210413/46901674-5bb9d100-cf14-11e8-8485-10dc21a2d06b.jpg)

###### `contacts-creator.component.html`

![](https://user-images.githubusercontent.com/210413/46901855-b3a60700-cf17-11e8-9828-f61c54e3b051.png)

## Bonus Tasks

1. Apply the same validator in the `ContactsEditorComponent` as well


## Next Lab

Go to [Forms Lab #4: Custom Async Validators](exercise-4_create-custom-async-validator-directive.md)

