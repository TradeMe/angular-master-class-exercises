## Exercise: Redux - Use a custom, redux-like Store

Redux promotes a simple one-way dataflow for applications 
where views dispatch actions, stores process actions using reducers
and then notify view listeners when the store state has changed.


## Scenario

Consider the following application where your clients can vote to increase the US Tea taxes.

![voter-app-with-redux](https://cloud.githubusercontent.com/assets/210413/25202424/fbc0e10c-251a-11e7-8247-485e70a2a059.jpg)


Let's simulate the Redux flow patterns using stores, reducers, and dispatched actions. 
This will be a simple emulation of the Redux synchronous functionality.

<br/>&nbsp;

![redux-emulation-voting-app](https://cloud.githubusercontent.com/assets/210413/25308498/34b09450-277b-11e7-898d-9c3c837d14d7.jpg)

<br/>&nbsp;

The AppStore class already has the store-like methods:

```ts
export class VoterStore {
   dispatch(action) { /* .... */ }
   subscribe(listener) { /* .... */ }
   getState(): any { /* .... */ }
}
```

## Tasks

1. Use the following actions to increment or decrement the votes:
    *  Add the actions (below) to the `src/app/store/voter-store.ts`  
    ```js
       export const VoteActions = {
         NO : "NO",
         YES : "YES"
       };
    ```
  
2. Update the **VoterComponent** to dispatch actions 
    * Dispatch VoteActions using plain objects with a `type` property   

3. Update `AppStore::reducer` to modify the store state for YES/NO actions.
    > Make sure you return a new state object instead of mutating the existing object!

4. See how the StatusComponent vote count changes as the vote buttons are clicked.

<br/>&nbsp;

## Next Lab

Go to [Step 2: Using the Redux Library](step-2-use-createStore.md)
