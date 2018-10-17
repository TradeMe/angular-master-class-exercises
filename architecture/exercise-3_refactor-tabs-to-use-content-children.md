## Lab 3: Refactoring the Tabs Component to use ContentChildren

In this exercise we'll revisit our approach to building a tab component and try out a different approach by access a component's children components using `ContentChildren`.

## Scenario

In the previous exercise we used the parent injection pattern to build a tab component consisting of two different elements `tab` and `tabs`.

```
<trm-tabs>
  <trm-tab title="General" fxLayout="column">
    ...
  </trm-tab>
  <trm-tab title="Address" fxLayout="column">
    ...
  </trm-tab>
</trm-tabs>
```

Turns out, that isn't the only way to implement such a thing. In fact there's a technique that is often superior using `ContentChildren`.

## Tasks

1. In `TabComponent` remove the `TabsComponent` and `OnInit` imports and remove all the affected code
2. In `TabsComponent` add imports for `ContentChildren`, `QueryList` and `AfterContentInit`.
3. Change the type of `tabs` from `Array<TabComponent>` to `QueryList<TabComponent>` and decorate it as `@ContentChildren(TabComponent)` as shown below.

  ```
  @ContentChildren(TabComponent)
  tabs: QueryList<TabComponent>;
  ```
4. Implement the `AfterContentInit` interface and call `this.select(this.tabs.first)` in its implementation method

## Code Snippets

###### `tabs.component.ts`

![a5](https://user-images.githubusercontent.com/210413/46903655-65ebc780-cf34-11e8-9e7f-02088d432c0a.jpg)

## Bonus Tasks

Our `TabsComponent` is great! However, it turns out, Angular Material comes with its own `MatTabs` component that comes with features like keyboard control and accessiblity. 

1. Let's refactor our ContactsEditor to use `MatTabs` instead of our custom `TabsComponent`. Read the component's [documentation](https://material.angular.io/components/tabs/overview) to learn how to do it.
  > Note: you will need to wrap your `mat-tab` content inside a **`<div fxLayout="column"></div>`**; since `mat-tab` will (by default) layout in a *horizontal* flow-direction.
  > &nbsp;<br/>
  > <img width="692" alt="screen shot 2017-06-06 at 11 31 34 am" style="padding-top:30px" src="https://cloud.githubusercontent.com/assets/210413/26807653/c84fe852-4aab-11e7-8f37-79e196e6ef40.png">


## Code Snippets

###### `contacts-editor.component.html`

![a3 1](https://user-images.githubusercontent.com/210413/47057248-4ac2d580-d21c-11e8-82cd-05b15ebee59a.jpg)


## Next Lab

Go to [Lab #4: App Global Communications](exercise-4_communicate-through-eventbus.md)
