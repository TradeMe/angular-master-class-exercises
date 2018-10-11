## Exercise: Redux - Use the Redux API

Instead of a custom redux-like emulator, let's use the Redux library and its field-tested
API to (a) build our Store and (b) manage action dispatching with 1...n reducers.

See http://redux.js.org/

## Scenario

Let's replace our custom, redux-emulator with a real Redux store and API usage.

<br/>&nbsp;

![redux-voting-app](https://cloud.githubusercontent.com/assets/210413/25308491/ed98ed10-277a-11e7-8d59-ac433b719c95.jpg)

To manage complexity (and demonstrate best practices), we will organize the voter functionality in a new package structure:

* `src/app/store/app-store.ts`
* `src/app/store/root-reducer.ts`
* `src/app/store/votes/vote-actions.ts`
* `src/app/store/votes/vote-reducer.ts`
* `src/app/store/votes/vote-state.ts`

## Tasks

1. Refactor the **AppStore** to group voter functionality in a common package:
   * Refactor (move) the `AppStore::VoteActions` to the module `src/app/store/votes/vote-actions.ts`
   * Refactor the `AppStore::reducer` method to a stand-alone function in `src/app/store/votes/vote-reducer.ts`:
    ```js
      /**
       * Use the custom actions to update the counter state!
       */
      export function voteReducer(state, action) {
        switch (action.type) {
          case VoteActions.NO  :  return {...state, counter: state.counter - 1};
          case VoteActions.YES :  return {...state, counter: state.counter + 1};
          default              :  return state;
        }
      }
    ```

  * **Delete** the `AppStore` class. Soon we will use the Store API and `createStore()`.


2. Implement custom VotesState in `vote-state.ts` as a model for the total votes.

   * Define **VotesState** interface:
   ```js
    export interface VotesState { counter : number }
   ```

   * Define an initial vote state; that will be used when creating the store.
   ```js
    export const INITIAL_VOTES_STATE : VotesState = { counter : 0 };
   ```

4. Update `vote-reducer.ts` imports to use the new VotesState and VoteActions

   * Specify the initial, default state in the **voteReducer** function
   ```js
    import {VoteActions} from './vote-actions';
    import {INITIAL_VOTES_STATE} from './vote-state';

    export function voteReducer(state = INITIAL_VOTES_STATE, action) { ... }
   ```

5. Create a root reducer `src/app/store/root-reducer.ts` to aggregate 1...n other reducers
   * Define a **ROOT_REDUCER** that is a hashmap of all custom reducers:
   * Define an **ApplicationState** interface to be used when creating the Store instance:
     > Note this interface only has  `votes : VotesState` property.

6. Now let's modify the **AppStore** to use the public Redux API and our **ApplicationState** interface:
   * Import the Redux **Store** and helper functions
   * Create a factory function that will build an instance of the Redux **Store** using our `voteReducer` function. 
     Use `combineReducer` to create a single, wrapper-reducer for the `createStore()` API
   * Create a unique injection token **APP_STORE** that will be used for future DI needs
   * Create an APP_STORE_PROVIDER that will use this **APP_STORE** token
  
7. Update the application DI to use the **APP_STORE_PROVIDER** implemented above. 
   * Import the new provider into `app.module.ts`:
   * Register the new provider with the application module DI system:

8. Modify the **VoterComponent** to use the injected Store and dispatch actions using our action creators
   *  Update the constructor to inject the new Store instance; using the **APP_STORE** token:
   *  Modify the `increment()` method to dispatch actions with the `type`:
   * Modify the `decrement()` method to dispatch the **VoteActions.NO** action

9. Update the **StatusComponent** to inject the new **Store** instance and :
   * Update the calls to `getState()` to access the `votes` property
   * Subscribe to reducer changes on the Store's ApplicationState 


<br/>&nbsp;

## Next Lab

Go to [Step 3: Using Action Creators](redux/step-3-use-action-creators.md)
