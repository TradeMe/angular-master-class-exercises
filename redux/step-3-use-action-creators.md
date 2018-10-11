## Exercise: Redux - Using Action Creators

When the same actions are used in many different places, **action creators** can be used to be more DRY. 

In general, Redux suggests that code with side effects should be part of the action creation process. While that logic can be performed inside of a UI component, it generally makes sense to extract that logic into a reusable function so that the same logic can be called from multiple places—in other words, an action creator function.

> Use of action creators is especially important when the object construction is non-trivial or when working with asynchronous actions. Note: we will use asychronous action creators in the lab exercise `Redux-Step-6: Using Thunks for Asynchronous Voting`.

For now, let's focus on [Synchronous Action Creators](http://redux.js.org/docs/advanced/AsyncActions.html#synchronous-action-creators)


## Tasks


1. Implement custom action creator functions in `vote-actions.ts`
    * Define **Action** interface:
    ```js
     export interface Action {
       type : any;
     }
    ```

    * Implement a synchronous action creator `voteYesAction():Action` 
    * Implement a synchronous action creator `voteNoAction():Action`

2. Modify the **VoterComponent** to use the injected Store and dispatch actions using our action creators
   *  Modify the `increment()` method to dispatch a custom actions instantiated by our action creator:
   * Modify the `decrement()` method to dispatch the **VoteActions.NO** action


<br/>&nbsp;

## Next Lab

Go to [Step 4: Using Middleware](redux/step-4-use-middleware.md)
