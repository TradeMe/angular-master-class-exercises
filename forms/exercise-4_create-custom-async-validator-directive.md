## Lab 4: Create async validator directive

In this exercise we'll explore how async validators are implemented in Angular. We'll learn how to create a validator that has service dependencies and how it needs to be added to the `NG_ASYNC_VALIDATORS` providers.

## Scenario

Email addresses should be unique. We shouldn't have multiple contacts that share the same email address. That's why we want make sure that, when a contact is added, the email address (if applied) isn't already used in an existing contact.

## Tasks

1. Add a method `isEmailAvailable(email)` to `ContactsService`
  - Use `http.get()` to send a request to `{API-ENDPOINT}/check-email?email={EMAIL}`
  - This endpoint returns
      - `{ error: 'NOT_AVAILABLE' }` - in case the given email address is in use
      - `{ msg: 'AVAILABLE' }` - in case the email address is available
2. Create a directive using angular-cli called `email-availability-validator`
3. Add a validator **factory** function `checkEmailAvailability(contactsService: ContactsService)` to `src/app/email-availability-validator.ts`.
4. Return the observable of `ContactsService#isEmailAvailable()`, make sure that it projects/emits the right next value, which is:
  - `null` - if the email address is available or,
  -  `{ emailTaken: true }` - if the email address is not available
5. Inject `ContactsService` into `EmailAvailabilityValidator`
6. Use `checkEmailAvailability()` as a factory function to store a validator on the class
7. Implement a method `validate(c: FormControl)` on `EmailAvailabilityValidator` which uses the new validator 
8. Change `EmailAvailabilityValidator`'s selector to  `[trmCheckEmailAvailability][ngModel]`.
9. Add the validator to `NG_ASYNC_VALIDATORS` using `forwardRef` and `useExisting` when configuring the provider
7. Apply `trmCheckEmailAvailability` directive to email input in `ContactCreatorComponent`s template
8. Display an error message accordingly

## Code Snippets

###### `contacts.service.ts`

![](https://user-images.githubusercontent.com/210413/46901722-0af6a800-cf15-11e8-89ac-c12e536cc9df.png)

###### `email-availability-validator.ts`

![f42](https://user-images.githubusercontent.com/210413/46901747-704a9900-cf15-11e8-9753-864970e8afa8.jpg)

###### `contact-creator.component.html`

![f43](https://user-images.githubusercontent.com/210413/46901907-83ab3380-cf18-11e8-89ea-a006a192ca05.png)

## Next Lab

Go to [Forms Lab #5: Refactor to Reactive Forms](exercise-5_refactor-to-reactive-forms.md)
