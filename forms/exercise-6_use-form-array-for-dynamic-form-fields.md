## Lab 6: Use FormArray for dynamic form fields

So far we've learned how to use reactive form APIs to create `FormGroup` and `FormControl`. While `FormGroup` represents a static known collection of `FormControl`s, Angular also enables us to great an unkown collection of `FormControl`s using the `FormArray` type.

`FormArray` is useful when we deal with forms, which structure can change at runtime.

## Scenario

A contact's structure  comes with several fields, including `name`, `email` or `birthday`. Another field is the `phone` field. While it's totally fine to have a contact with just a single phone number, it's nowadays very common that a contact can have multiple numbers for different platforms. Let's change `ContactCreatorComponent` to use `FormArray` so we can dynamically add `FormControl`s for `phone`.

## Tasks

1. Import `FormArray` and `FormControl` from `@angular/forms` in `contacts-creator.component.ts`
2. Change the `phone` field to be a `FormArray` using `FormBuilder#array()`
3. Change `ContactsCreatorComponent` template to render multiple phone numbers. You can use the snippet below
4. Make sure to insert the correct expression so `NgFor` outputs multiple templates
5. Add the correct `[formControlName]` binding
6. Implement `addPhoneField()` method in `ContactsCreatorComponent`
7. Implement `removePhoneField(index)` method in `ContactsCreatorComponent`

## Code Snippets


###### `contacts-creator.component.html`

```html
<div formArrayName="phone">
  <div *ngFor="INSERT_EXPRESSION">
    <mat-form-field>
      <input matInput placeholder="Phone">
    </mat-form-field>
    <button
      mat-icon-button
      type="button"
      *ngIf="i >= 1"
      (click)="removePhoneField(i)"><mat-icon>highlight_off</mat-icon></button>

    <button
      mat-icon-button
      type="button"
      *ngIf="l && phone.value != ''"
      (click)="addPhoneField()"><mat-icon>add_circle_outline</mat-icon></button>
  </div>
</div>
```

###### `contacts-creator.component.ts`

![group 14](https://user-images.githubusercontent.com/210413/46901958-4004f980-cf19-11e8-9410-cf136d3aef1d.jpg)

## Bonus Tasks

1. Try to apply the same things to `ContactsEditorComponent`

## Next Lab

Go to [Forms Lab #7: Create custom form control](exercise-7_create-custom-form-control.md)

