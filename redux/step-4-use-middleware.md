## Exercise: Redux - Use Redux Middleware

Analogous to a plug-in architecture, Redux supports a 3rd-party interception plugin architecture known as **middleware**.
This middleware serves as a layer between dispatching an action and the reducer(s) which will process that action.

People use Redux middleware for logging, crash reporting, talking to an asynchronous API, routing, and more. Middleware 
processes are functions which intercept the action before it is delivered to 1..n reducers. These functions called interceptors.

<br/>&nbsp;

![middleware-interceptors](https://cloud.githubusercontent.com/assets/210413/25308489/ea1b8e72-277a-11e7-91d9-36c0b8d12f3e.jpg)

## Scenario

Let's extend our application to log the actions to add and remove votes. Instead of monkey-patching
the dispatcher or the store, we will use the middleware features to chain 1...n action interceptors.

<br/>&nbsp;

![MiddleWare Logging](https://cloud.githubusercontent.com/assets/210413/25308450/1ee3efb0-277a-11e7-96fe-c5a2663314d0.png)


## Tasks

1. Create a `/src/app/store/middleware.ts` module for our middleware functions.
   * Define a `logger` interceptor function to log action activity and chain the action:  
    ```js
      export const logger = store => next => action => {
        console.group('Redux Middleware [logger];');
          console.log('dispatching', action);
            let result = next(action);
          console.log('next state ', store.getState());
        console.groupEnd();
        
        return result;
        
      };
    ```
   * Define a `crashReporter` interceptor function to catch exceptions, log, and rethrow:
    ```js
      export const crashReporter = store => next => action => {
        try {
        
          console.group('Redux Middleware [crashReporter]:')
            console.log('dispatching', action);
              let result = next(action);
            console.log('next state ', store.getState());
          console.groupEnd();
          
          return result;
          
        } catch (err) {
          console.error('Caught an exception!', err);
          throw err;
        }
      };
    ```

2. Update the store construction to register the custom middleware functions. Chain the functions
   in the order desired:   
   *  Import the `applyMiddleware()` function that will be used to register the custom interceptors:
   *  Import the custom middleware, interceptor functions into the `store/app-store.ts` module: 
   *  Using `applyMiddleware()` to register the functions when the store is created:


<br/>&nbsp;

## Next Lab

Go to [Step 5: Using Thunks for Async Actions](redux/step-5-thunks-for-async-voting.md)
