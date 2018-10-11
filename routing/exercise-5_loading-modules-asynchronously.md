## Lab 5: Lazy Loading Modules

Instead of loading every application part upfront we can specify to load specific  modules asynchronously to only fetch the files when a particular route gets activated.

Luckily, Angular's router supports lazyloading `NgModules`, which makes loading modules at runtime a breeze.

## Scenario

Considering that our about page may be rarely viewed, we like to cut of the initial size of our app by fetching the `AboutComponent` asynchronously once the route becomes active.
To do that, we need to create a new `NgModule` (let's say `AboutModule`), which declares the `AboutComponent`. The `AboutModule` can then be lazyloading using a routes config's `loadChildren` function.


  ```
  $ ng g m about
  ```
  
## Tasks

1. Create a new "About" `NgModule` using the Angular CLI 
2. Remove `AboutComponent` from `ContactsModule`s declarations and remove the import as well
3. Import `AboutComponent` in `about.module.ts` instead and add it to `AboutModule`'s declarations.
4. Import `RouterModule` in `about.module.ts` and configure a default route for the `AboutModule` that points to `AboutComponent`, using `RouterModule.forChild(...)`
5. In order to keep the UI working, we need to add `FlexLayoutModule` and `ContactsMaterialModule` to `AboutModule`s imports as well
6. Change the root route configuration for path `about` to use `loadChildren` instead


## Code Snippets

###### `about/about.module.ts`

![r5 1](https://user-images.githubusercontent.com/210413/46908723-93139680-cf83-11e8-98b7-894c61d10e1c.jpg)

###### `app.routes.ts`

![r5 2](https://user-images.githubusercontent.com/210413/46908721-93139680-cf83-11e8-8211-aa1ebb4f28e0.jpg)

