# Exercise: Testing Inputs and Outputs

Let's take it a step further and test and actual Angular Component. In this lab we want to explore the APIs needed to test Component Inputs and Outputs.

## Scenario

Our `ContactsDetailComponent` comes with Inputs and Outputs to receive contact data and to notify the outside world about any action inside the component. Those inputs and outputs can be tested using Angular's testing APIs `fixture`, `debugElement` and `triggerEventHandler`. Let's write some test that check whether our inputs and outputs work as expected!

## Tasks

0. Create a new file `contacts-detail/contacts-detail.component.spec.ts`
1. Create a new `describe()` block for `ContactsDetailComponent`
2. Create a `beforeEach()` block in which we initialize `TestBed.configureTestingModule()`
  - Create testing module using `TestBed.configureTestingModule()`
  - Create component fixture using `TestBed.createComponent()`
  - Initialize component instance from fixture
3. Write a test that checks whether `ContactsDetailComponent` renders a contact from its input
  - Assign contact object to the component's instance `contact` property
  - Perform change detection using `fixture.detectChanges()`
  - Use `fixture.debugElement` to query `mat-card-title`. Check for the contact's name in the title
4. Write a test that ensures `ContactsDetailComponent` emits a `back` event
  - Use `fixture.debugElement` to query for `mat-button`
  - Subscribe to `component.back` (this is the output property of `ContactsDetailComponent`
  - Call `triggerEventHandler('click', null)` on the queried button
5. Write a test that checks whether `ContactsDetailComponent` emits an `edit` event
  - Use the same steps as in step 4) but subscribe to the `edit` event
  - ensure `edit` emits the expected contact object


