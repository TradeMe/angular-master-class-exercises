## Exercise: Using @ngrx/entity

@ngrx/entity provides utilties to handle CRUD operations and queries for your collections.
  
## Scenario

Let's change our `contacts.reducer.ts` to use @ngrx/entity adapters and EntityState. 
Then update your `contacts.selectors` to use @ngrx/entity selectors.
 
## Tasks

1. In **`contacts.reducer.ts`** 
  * use EntityState and EntityAdapter to define your feature state.
  * use `adapter.getInitialState()` to build your initial state
  * update your reducer to use `adapter.addAll()` and `adapter.upsertOne()`
2. Update your **`contacts.selectors`**
  * use `adapter.getSelectors()`
3. Update your **`contacts-ngrx.module.ts`** use the `getContactsInitialState` function to build the initialState 

## Code Snippets

##### `contacts.reducer.ts`

![ngrx9 1](https://user-images.githubusercontent.com/210413/47192883-5b09ba80-d3ac-11e8-85ad-cd6cbfae61fd.jpg)

![ngrx9 2](https://user-images.githubusercontent.com/210413/47192882-5b09ba80-d3ac-11e8-8456-f296c32feb6b.jpg)


##### `contacts.selectors.ts`

![ngrx9 3](https://user-images.githubusercontent.com/210413/47192881-5a712400-d3ac-11e8-9fab-e514fa01fbda.jpg)

##### `contacts-ngrx.module.ts`

![ngr9 4](https://user-images.githubusercontent.com/210413/47192992-19c5da80-d3ad-11e8-905b-dd9389ee3fd3.jpg)


## Next Lab

Congratulations! You are done.
