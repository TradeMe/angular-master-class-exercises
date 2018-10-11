# Exercise: Angular Universal for Server-Side-Rendering

A "normal" Angular application executes in the browser and renders pages dynamically in response to user actions, e.g. clicking on a button that brings us to our user profile.

When using [Angular Universal](https://universal.angular.io/) generates the pages of our application statically on the server through a process called server-side rendering (SSR).

There are two approaches. Either we statically pre-render our pages as HTML files during a build step and then serve them from our web server, or generate and pre-render those pages on the server in response to requests from the browser.

## Scenario

Let's use Angular Universal to generate our pages on the server side and serve them through our own little Expess.js server.

## Tasks

This exercise is a little bigger and is divided into two parts.

In the first part we'll add everything we need in order to build the client and server bundle, making our app SSR friendly.

In the second part we build a little Express.js web server which takes care of rendering our application using Angular Universal on the server-side and serving the generated static HTML.

### Part 1

1.  Normally you start by adding the required dependencies. However, this is done already so we can skip this part.
2.  Let's start by making our `ContactsModule` compatible with Angular Universal. For that we simply call `.withServerTransition({ appId: 'trm-contacts-app' })` on the already existing `BrowserModule`. Calling this method allows the browser-based application to transition from a server-rendered app using the given `appId`.
3.  Next, create a dedicated module called `AppServerModule` which is used to bootstrap the application on the server.

* Create a new file `app.server.module.ts` alongside the `app.module.ts`, meaning in the same folder.
* Implement a new `NgModule` and call in `AppServerModule`. This is an Angular module that wraps the application's root module (`ContactsModule`) so that Universal can mediate between your application and the server.
* Add the following imports:
  * `ServerModule` from `@angular/platform-server`
  * `ModuleMapLoaderModule` from `@nguniversal/module-map-ngfactory-loader`
  * `FlexLayoutServerModule` from `@angular/flex-layout/server`
  * `ContactsModule` and
  * `ContactsAppComponent`
* Add those imports to the list of imports of the server module.
* Add the `ContactsAppComponent` to the list components that should be bootstrapped.

4.  Create a `main.server.ts` which is the entry point for running the app our server. Simply export the `AppServerModule`.

5.  Create a new `tsconfig` specifically for the server-side application. This will configure TypeScript and AOT complilation of the Universal app. Use the following content:

```
{
  "extends": "../tsconfig.json",
  "compilerOptions": {
    "outDir": "../out-tsc/app",
    "baseUrl": "./",
    "module": "commonjs",
    "types": []
  },
  "exclude": [
    "test.ts",
    "**/*.spec.ts"
  ],
  "angularCompilerOptions": {
    "entryModule": "app/app.server.module#AppServerModule"
  }
}
```

* Important here is to use **commonjs** for the `module` property, as well as the `angularCompilerOptions` property which guides the AOT compiler. The latter tells the compiler which of our modules is the entry point.

6.  Create a new target inside the `angular-cli.json`.

* Inside the `angular-cli.json` there's an object under the key `architect` under `projects/contacts-app`. Use the following object and add it to your CLI configuration:

```
"server": {
  "builder": "@angular-devkit/build-angular:server",
  "options": {
    "outputPath": "dist/server",
    "main": "src/main.server.ts",
    "tsConfig": "src/tsconfig.server.json"
  }
}
```

7. Update the `outputPath` of your `build` target inside your `angular-cli.json`. Change it to `dist/browser`.

8.  With all of the above, we can already build both the client and server bundle. Run `npm run build:ssr` or with yarn `yarn build:ssr`. This should build both bundles and put the build artifacts in `dist`. There should be two folders, `browser` and `server`.

### Part 2

1.  In the first lab we already created a simple web server. In this lab we take that file `server/server.ts` and replace the content with our Angular Universal implementation. So go ahead and delete everything from that file to start fresh.

2.  Add the following imports to the top of the file:

```
import 'zone.js/dist/zone-node';
import 'reflect-metadata';

import { enableProdMode } from '@angular/core';

import * as express from 'express';
import { ngExpressEngine } from '@nguniversal/express-engine';
import { provideModuleMap } from '@nguniversal/module-map-ngfactory-loader';
import { join } from 'path';

// NOTE: leave this as require() since this file is built Dynamically from webpack
const { AppServerModuleNgFactory, LAZY_MODULE_MAP } = require('../dist/server/main');
```

3.  Enable the prod mode by calling `enableProdMode()`.

4.  Create a new express instance and assign it to a variable called `app`.

5.  Set up two variables, one for the port (similar to what you did in the first lab) and the other one for the dist folder. You can use a very convenient cross platform method called `join` which concatenates several segments into one path, like so `join(process.cwd(), 'dist')`.

6.  Tell express to use the `ngExpressEngine` for `html` files using `app.engine('html', ngExpressEngine({...}))`. The `ngExpressEngine` is actually just a wrapper around Angular Universal's `renderModuleFactory` that turns a client's request into server-rendered HTML pages. `ngExpressEngine` takes a configuration object with two properties, `bootstrap` and `providers`.

* Set the `bootstrap` property to `AppServerModuleNgFactory`. Here we use the factory file of our `AppServerModule` which is the output of the AOT compiler.

* Add `provideModuleMap(LAZY_MODULE_MAP)` to the list of providers. This is an additional provider so that we can get lazy-loading to work differently as we don't need to fetch the module via an HTTP request but rather just instantly render it.

7.  Set the `view engine` to `html`:

`app.set('view engine', 'html');`

8.  Tell express where our views are located:

`app.set('views', join(DIST_FOLDER, 'browser'));`

9.  Set up a route for get requests to serve static assets like images:

`app.get('*.*', express.static(join(DIST_FOLDER, 'browser')));`

10. Set up another `get` listener for all other routes. Here you can use `*` as a route which matches all regular routes, essentially everything that has no `.` in the requested path. Return the rendered `index.html` in the callback:

`res.render(join(DIST_FOLDER, 'browser', 'index.html'), { req });`

11. Finally, bind the app to the configured port to start our web server.
12. To test if everything works as expected, we can now build the bundles and serve the app through our Express server.

* Simply run `npm run serve:ssr`. This will build both bundles, start the web server and serve our contacts application.

Congrats! If you have successfully followed the steps above, the contacts application should be server-side rendered and the page should show up much faster. Also note that the `index.html` served by our web server already includes the contacts requested from the REST API. Also, with Angular Universal, when the browser gets the HTML file, we don't have to wait until Angular kicks in and generates our page on the fly in the browser. This all happened on the server side already leading to a much faster meaningful inital paint.

**Note**: Please don't use this server for production apps as it's not secure and doesn't have authentication and security things setup!

**Tip:** In your own applications you don't have to do these steps by hand. If you are using the Angular CLI you can simply run `ng g universal` which will do all that for you (without implementing the actual server). We did this by hand to understand each step and get to know what's going on.
