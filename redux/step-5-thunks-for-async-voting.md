## Exercise: Redux - Use Thunks with Asynchronous Actions

Without middleware, Redux store only supports **synchronous** data flows. This is what you get by default with createStore().

Asynchronous middleware like **redux-thunk** allows you to dispatch something other than actions, for example, functions. Any middleware you use can then interpret anything you dispatch, and in turn, can pass actions to the next middleware in the chain. 

For example, a Function middleware can intercept Functions. When the last middleware in the chain dispatches an action, it has to be a plain object. This is when the synchronous Redux data flow takes place.

<br/>&nbsp;

![redux-middleware-async](https://cloud.githubusercontent.com/assets/210413/25308705/ed3825e8-277f-11e7-822f-0510ab133a32.jpg)

## Scenario

Let's extend our application to use a REST serve to manage votes and log the action to show the total votes from the server. 

We will use **redux-thunk** to process action **functions** in our middleware layers.

<br/>&nbsp;

![async voting with middleware ](https://cloud.githubusercontent.com/assets/210413/25308725/e6053e54-2780-11e7-8f26-dc7951cd8804.png)

> Notice that only the synchronous VoteAction.LOADED is logged by the middleware. 
The async actions are processed by the **thunk** processor.

## Tasks

1. Create a `/src/app/store/votes/voter-service.ts` module for our REST service calls.

   ```js
	import { Injectable } from '@angular/core';
	import { Http } from '@angular/http';

	import 'rxjs/add/operator/toPromise';
	import 'rxjs/add/operator/map';

	@Injectable()
	export class VoterService {
	  constructor(private http: Http) {}

	  getVotes () {
		return this.http
			.get('http://localhost:4201/api/votes')
			.map(res => res.json().votes);
	  }

	  addVote () {
		return this.http
			.get('http://localhost:4201/api/votes/increment')
			.map(res => res.json().votes);
	  }

	  removeVote() {
		return this.http
			.get('http://localhost:4201/api/votes/decrement')
			.map(res => res.json().votes);
	  }
  	};
   ```

2. In `app-module.ts`, Register the **VoterService** as a provider for the application:

3. In `app-store.ts`, import and register the **thunk** middleware:
   ```js
    import thunk from 'redux-thunk';
   ```
   * Register the **thunk** with the `applyMiddleware()` feature.

4. In `votes/vote-actions.ts` prepare our **asynchronous** action creators:
   * Extend our action interface to support vote counter and VoterService references
     as payload options:
   ```js
    import {VoterService} from './voter-service';
  
    export interface Action {
      type     : any;
      counter ?: number;          // returned from REST server
      service ?: VoterService;    // need by the async functions
    }
  
    /**
     * VoteAction Constants
     */
    export const VoteActions = {
      VOTES_LOADED: "LOADED"      // Sync action
    };
  
    // *************************************************
    // Implement Synchronous Action Creators
    // *************************************************
  
    export function votesLoadedAction(counter:number):Action {
      return { type : VoteActions.VOTES_LOADED, counter };
    }
   ```
  
   * Implement asynchronous action creators; which return **function**s 
     instead of plain objects.
   ```js
	    // NOTE: `getState` is an optional argument
	    
	    export function voteYesAction(service:VoterService) {
	      return (dispatch, getState) => {		
		// Call voterService and dispatch its response
	      };
	    }

	    export function voteNoAction(service:VoterService) {
	      return (dispatch, getState) => {
		// Call voterService and dispatch its response
	      };
	    }
   ```

5. In `votes/vote-reducer.ts`, update the reducer function to handle only `VoteActions.VOTES_LOADED`:
   ```js
   export function voteReducer(state:VotesState = INITIAL_VOTES_STATE, action:Action) {
     switch (action.type) {
	case VoteActions.VOTES_LOADED : return {...state, counter: action.counter };
	default                       : return state;
     }
   }
   ```

6. In **VoterComponent**, use the async action creators and send the required **VoterService**:

<br/>&nbsp;

---- 

### REST Server

This Angular application now uses HTTP to connect to a remote Voter REST service (available `http://localhost:4201/api/votes`).

Be sure to start your local NodeJS Voter server using `npm run vote-server`.



<br/>&nbsp;

## Next Lab: Part 2 (ngrx)

Go to [Step 1: Using **ngrx**](ngrx/step-1-use-ngrx.md)
