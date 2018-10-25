## Exercise: Apply Meta-Reducers

Similar to redux, ngrx also supports "middleware" or rather **meta-reducers** or **enhancers**. Meta-reducers serve as a layer between all dispatched actions and the reducer(s). It can be used for anything from logging, asynchronous event handling, or ensuring immutability by deep freezing the store object.

We will also use the Redux DevTools to explore the state changes and time travel within our application:

![screen shot 2017-04-24 at 4 25 10 pm](https://cloud.githubusercontent.com/assets/210413/25603083/96216562-2ebe-11e7-97eb-7210dc6a62b2.png)

## Scenario

Use the build environment to differentiate production vs development builds. Then create an array of meta-reducers that includes `storeFreeze`, a meta-reducer that prevents the state from being directly mutated.

## Tasks

1. Add or update the following imports in `src/app/state/app.state.ts`:

    ```js
    import { storeFreeze } from 'ngrx-store-freeze';
    import { environment } from '../../environments/environment';
    ```

2. Create and export a const variable called `META_REDUCERS` and, depending on `environment.production`, assign it an array of meta-reducers or an empty array.

    * If the environment variable evalutes to `false`, return an array that includes `storeFreeze`.
    * Otherwise return an empty array.

4. Update `app.module.ts` to import our `META_REDUCERS`.

    ```js
    import { ROOT_REDUCER, META_REDUCERS } from './state/app.state.ts';
    ```

5. Pass the meta-reducers to `StoreModule.forRoot()` via the `StoreConfig` as a second parameter.

    ```js
    StoreModule.forRoot(ROOT_REDUCER, {
      metaReducers: META_REDUCERS
    }),
    ```

6. Add `StoreDevtoolsModule` to the imports in `app.module.ts` and call `instrument()` with the following options:

    * Import `StoreDevtoolsModule` from `@ngrx/store-devtools`.

    ```js
    StoreModule.forRoot(ROOT_REDUCER, {
      metaReducers: META_REDUCERS
    }),
    !environment.production ? StoreDevtoolsModule.instrument({ maxAge: 5 }) : [],
    ```

    > We only want to add the `StoreDevtoolsModule` if the environment is **not** production. Otherwise we return an empty array.

7. Install [Redux DevTools](https://chrome.google.com/webstore/detail/redux-devtools/lmhkpmbekcpmknklioeibfkpmmfibljd) chrome extension to power-up your development workflow and enable time travelling and much more.

## Next Lab

Go to [Step 6: Using Effects for Asynchronous Actions](step-5-async-with-effects.md)

## Technical Considerations

The `forRoot` function of the `StoreModule` takes a map of reducers as a first argument and a store configuration object as a second argument. Using the `StoreConfig` we can provide ngrx with a list of meta-reducers. If there are no meta-reducers then ngrx will simply call `combineReducers` which basically iterates over all object keys of the reducer map and calls the reducer function to generate the value for each property in the store.

However, if we specify a list of meta-reducers, ngrx will **not** call `combineReducers` right away to generate a single root reducer but compose our reducer map together with the meta-reducers into a root meta-reducer.

The composition itself can be presented as an array of functions: `[A, B, C, combineReducers]`. Note that the last function of the array will always be `combineReducers`. This is handled by ngrx and happens behind the curtain. We **don't** have to take care of this. Internally, ngrx will `compose` this array of meta-reducers into a root meta-reducer. This `compose` function reduces the array from right to left resulting in a single function. This function is called root meta-reducer.

Whenever an action is dispatched the root meta-reducer is called. This means that all of our "middleware" functions are called from left to right.

The result of each intermediate step is passed on to the next meta-reducer.

Finally `combineReducers` is called.
