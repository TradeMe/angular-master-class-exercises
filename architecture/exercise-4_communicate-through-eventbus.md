## Lab 4: Global Communicate via custom event bus

In this exercise we like to build a generic event bus to do inter-component communication in a generic and reusable way.

![architecture-step-2-solution](https://cloud.githubusercontent.com/assets/210413/17643463/96900852-6130-11e6-8e1f-7e116b99f9c8.png)

## Scenario

We want to create an `EventBusService` with the following two APIs.

`EventBusService#emit(eventType: string, data: any)`

`EventBusService#observe(eventType: string) -> Observable<any>`

With this service and its two APIs we have a central place to emit events of any event type with any data. We can also observe messages passed through the bus from any place that has access to the `EventBusService`.

Use the EventBusService to update the application `title` based on the current, routed/active view.
## Tasks

1. Create an `EventBusService` using angular-cli
	1. Import `Observable` from `rxjs`
	2. Import `Observer` from `rxjs`
	3. Import `Subject` from `rxjs`
	4. Create an interface `EventBusArgs` with a field `type` of type `string` and a field `data` of type `any`
	5. Create a new `Subject` generic of type `EventBusArgs` on a `messages` property
	6. Implement a method `emit(eventType: string, data: any)` which emits on the subject
	7. Implement a method `observe(eventType: string) -> Observable<any>` which filters on the subject
	
9. Add `EventBusService` as a provider to our application module
10. Import and expose the `EventBusService` on the `ContactsAppComponent`
11. Observe the `appTitleChange` event and inject the current title on the `title` property
    ```
      ngOnInit () {
        this.eventBusService.observe('appTitleChange')
                          .subscribe(title => this.title = title);
      }
    ```
12. For each of the router-outlet views, import the `EventBusService` and emit the `appTitleChange` event with the desired value on all relevant code paths


## Code Snippets

###### `event-bus.service.ts`

![a6](https://user-images.githubusercontent.com/210413/46903735-9122e680-cf35-11e8-9512-68e0b588462d.jpg)


###### `app.component.ts`

![a7](https://user-images.githubusercontent.com/210413/46903766-0d1d2e80-cf36-11e8-830e-e70d3c3171aa.jpg)

