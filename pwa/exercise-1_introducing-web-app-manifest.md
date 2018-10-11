# Exercise: Introducing Web App Manifest

The term "Progressive Web App" can be really considered an umbrella term that represents different characteristics of a web app. One of those characteristics is that the app is installable.

With web app manifests we can tell the browser our web app can be added to the home screen and provide additional meta data to offer a good end user experience.

## Scenario

Let's add a web app manifest to our contacts app to slowly transform it into a progressive web app!

## Tasks

1. Add a `<meta name="theme-color">` to our app's `index.html` to make mobile browsers theme the app accordingly.
2. Create a `manifest.json` in `src/assets` and add the following properties:
  - `name` - Name of the app
  - `short_name` - Name to be used by app install banner
  - `icons` - A list of icon objects with the structure:
    - `src` - Path to an icon (usually `/assets/favicons/*`)
    - `sizes` - Dimensions of the icon
    - `type` - File type (`image/png` in out case)
  - `theme_color` - Same color as used for the meta tag
  - `background_color` - Background color for splash screen
  - `display` - Can be `standalone` or `browser`
  - `orientation` - Can be `landscape` or `portrait`
  - `start_url` - Entry point of application

Use the Chrome Devtools to test if your manifest works!

### Additional resources and help

- [Web Fundamentals - Web App Manifest](https://developers.google.com/web/fundamentals/web-app-manifest/)

