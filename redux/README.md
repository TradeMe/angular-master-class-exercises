## Lab Exercises

*  [Step 1: Redux Emulation](redux/step-1-redux-emulator.md)
*  [Step 2: Using the Redux Library](redux/step-2-use-createStore.md)
*  [Step 3: Using Action Creators](redux/step-3-use-action-creators.md)
*  [Step 4: Using Middleware](redux/step-4-use-middleware.md)
*  [Step 5: Using Thunks for Async Actions](redux/step-5-thunks-for-async-voting.md)

Redux promotes a simple one-way data flow for applications; where views dispatch actions,
stores process actions using reducers and then notify view listeners when the store state has changed.

For our application, we can see below how:

*  the View is composed of nested components.
*  the **StatusComponent** view on subscribes/watches the **Store** for vote changes
*  the **VoterComponent** view dispatches actions to the **Store**.

![redux_voter_flow](https://cloud.githubusercontent.com/assets/210413/25229730/0acdd494-2597-11e7-8852-91f3527ac2f9.jpg)

## Scenario

To explore the concepts of the Redux patterns, let's use the following Angular application where visitors can vote to support the Tea Tax Act passed in 1773 by Parliment, England.

![VoterApplication](https://cloud.githubusercontent.com/assets/210413/25202424/fbc0e10c-251a-11e7-8247-485e70a2a059.jpg)

Let's use the Redux API to build an simple Voting application using stores, reducers, dispatched actions, and middleware.
