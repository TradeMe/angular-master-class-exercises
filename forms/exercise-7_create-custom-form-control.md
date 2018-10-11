## Lab 7: Create custom form control

Native HTML form controls are usually very good at what they are doing. They are accessible and are well supported in modern browsers. However, sometimes we want to build more sophisticated controls, or simply reuse existing form logic. That's where custom form controls come into play.

## Scenario

You might have noticed that `ContactsCreatorComponent` and `ContactsEditorComponent` are very similar. A lot of logic is redundant, which is usually a good sign to refactor things. Let's start with small steps and refactor all address related fields into a custom form control, so it can be reused in both components, without reimplementing them more than once.

  ```console
  $ ng g c address-input
  ```

## Tasks

1. Create a new component `AddressInputComponent` using Angular CLI
2. Change its template to render address related form fields:
3. Import `ControlValueAccessor`, `FormGroup`, `FormBuilder` and `NG_VALUE_ACCESSOR` from `@angular/forms`
4. Create a multi provider for the token `NG_VALUE_ACCESSOR` that registers `AddressInputComponent` using `useExisting` provider strategy and `multi: true`
5. Make `AddressInputComponent` implement `OnInit` and `ControlValueAccessor`
6. Inject `FormBuilder` instance into `AddressInputComponent`
7. Create a form in `ngOnInit()` that has all the form controls the template needs
8. Implement `writeValue(address: Address)`
9. Implement `registerOnChange(fn)` and `registerOnTouched(fn)`
10. Subscribe to form value changes and call your registerd change handler whenever the form emits a change
11. Call onTouched handler whenever any of the form controls emit a `blur` event
12. Use `AddressInputComponent` in `ContactsCreatorComponent` and `ContactsEditorComopnent`
  > 
```html
      <trm-address-input formControlName="address"></trm-address-input>
```

> Don't forget to register this custom form control in your module declarations!

## Code Snippets


###### `address-input.component.html`

```html
<fieldset [formGroup]="form" fxLayout="column">
  <legend>Address</legend>
  <mat-form-field fxFlex>
    <input matInput placeholder="Street" (blur)="propagateTouch()" formControlName="street">
  </mat-form-field>
  <mat-form-field fxFlex>
    <input matInput placeholder="Zip" (blur)="propagateTouch()" formControlName="zip">
  </mat-form-field>
  <mat-form-field fxFlex>
    <input matInput placeholder="City" (blur)="propagateTouch()" formControlName="city">
  </mat-form-field>
  <mat-select placeholder="Country" (blur)="propagateTouch()" formControlName="country">
    <mat-option *ngFor="let country of countries" [value]="country.name">{{ country.name }}</mat-option>
  </mat-select>
</fieldset>
```

###### `address-input.component.ts`

![group 15](https://user-images.githubusercontent.com/210413/46901983-aa1d9e80-cf19-11e8-9942-9224c0ac2792.jpg)

