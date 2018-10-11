## Lab 2: Inject Parent into View Children

In this exercise we're going to build a generic Tab component. To be more specific we'll build a `tab` and a `tabs` component that work together as shown below.

```html
<trm-tabs>
  <trm-tab title="General">
    ...
  </trm-tab>
  <trm-tab title="Address">
    ...
  </trm-tab>
</trm-tabs>
```

We'll apply the parent injection pattern to make that work.

## Scenario

The `ContactsEditorComponent` shows general information as well as an address for each contact. With this exercise we want to build a tab component to display the general info and the address in two seperate tabs rather than one below the other.


## Tasks

1. Create a new directory `tabs` inside your `app` directory
2. Go into the `tabs` directory and generate a `tab` and a `tabs` component
3. The markup for the `TabsComponent` loops through an array of `tab` instances to construct a list of tab headers. It uses content projection to project the actual `tab` elements so that they sit below the header.
4. The markup for the `TabComponent` is really simple. It uses content projection to display whatever is between the opening and the closing `tab` tag.

  ```
  <ng-content *ngIf="selected"></ng-content>
  ```
5. Create a boolean property `selected` as well as an string property `title` on the `TabComponent`
6. Import the `@Input` decorator and apply it to the `selected` and `title` property
7. Import the `TabsComponent` and use it as a typed parameter in the constructor. This will inject the `TabsComponent` instance which is a direct parent of the `tab` component in the DOM tree
8. In the `TabsComponent` implement a method `addTab(tab: TabComponent)` which takes a tab instance and puts it into a local array. We can think of it as a way to register instances of `TabComponent` at the `TabsComponent`
9. Implement a `select(tab: TabComponent)` method in the `TabsComponent` that sets `selected` to `false` for all tabs except the one that was passed by the caller
10. Make sure to call `select(tab: TabComponent)` for the first tab that gets registered
11. Use `<trm-tabs>` and `<trm-tab>` in the markup of the `ContactsEditorComponent` to reorganize the content in tabs.

## Code Snippets

###### `tabs.component.html`

![a3](https://user-images.githubusercontent.com/210413/46903560-56b84a00-cf33-11e8-9fd6-9752a999d429.jpg)

###### `tabs.component.ts`

![a4](https://user-images.githubusercontent.com/210413/46903581-9e3ed600-cf33-11e8-990a-a032ea2a2c5e.jpg)

###### `contacts-editor.component.html`

![a2](https://user-images.githubusercontent.com/210413/46903530-d4c82100-cf32-11e8-8acf-c7c8f8289cbc.jpg)

## Next Lab

Go to [Lab #3: Using ContentChildren Query](exercise-3_refactor-tabs-to-use-content-children.md)

