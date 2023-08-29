# Astrolytics.io React Native SDK

![Astrolytics.io](https://intriguing-lemonade-efa.notion.site/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F98020d0c-fd01-43ff-a29e-8f1c8f30de4b%2Fmsdncsmcnsm.jpg?table=block&id=db0f27a3-321c-400e-9ca7-db0213d1dee1)

## Table of Contents

1. [Getting Started](#getting-started)
2. [Usage](#usage)
3. [How to Contribute](#how-to-contribute)

## Getting Started

To get started with Astrolytics, create an account at [Astrolytics](https://dash.astrolytics.io/login) and grab the App ID, then
use the SDK to start tracking events.

### Installation

This package has `@react-native-async-storage/async-storage` and `@react-native-community/netinfo` as peer dependencies. Install them first if you don't have them

```bash
yarn add @react-native-async-storage/async-storage @react-native-community/netinfo
```

then proceed to install `astrolytics-rn` As NPM package (recommended)

```bash
# with yarn
yarn add astrolytics-rn
```

### Usage


```javascript
import Astrolytics from 'astrolytics-rn';

Astrolytics.init('YOUR_APP_ID');
```

Replace `'YOUR_APP_ID'` with the unique ID of your app. You can get it [here](https://dash.astrolytics.io/account).

You can check examples with different frameworks [here](./playground).

## API

Astrolytics supports passing the following options as second argument to the `Astrolytics.init()` method:

```js
Astrolytics.init('APP_ID', {
  appVersion: '0.0.0', // the version of your application
  endpoint: 'wss://app.astrolytics.io', // only option, we don't allow self hosting yet :(
  disableInDev: true, // disable in development mode. We recommend not to call
                      // `init` method, as that will be more reliable.
  debug: false, // if set to `true`, will log a bunch of things.
  disableTracking: false, // will not track anything. You can also use `Astrolytics.disableTracking()`.
                          // note that some events will still be added to the queue, so if you call
                          // Astrolytics.enableTracking() again, they will be sent to the server.
  reportInterval: 2 * 1000, // at which interval the events are sent to the server.
  sessionTimeout: 60 * 30 * 1000, // time after which the session is ended
  cutoff: 60 * 60 * 48 * 1000, // time after which event that were not sent yet are deleted
  disableErrorReports: false, // wether to disable error tracking
})
```

### Tracking

Track events with optional custom data

```javascript
Astrolytics.track("click", { foo: 'bar' });
```

### Error Tracking

Track errors with a name and the Error object.

```javascript
Astrolytics.trackError(name, error);
```

By default Astrolytics registers a handler for `ErrorUtils.setGlobalHandler` that sends `'GlobalError'` errors to the API. If you want
to disable this behaviour, you can set `disableErrorReports` to `true`:

```js
Astrolytics.init('APP_ID', { disableErrorReports: true })
```

and catch errors manually using `Astrolytics.trackError('an error', errObject)`.

### User Identification

Identify a user by a unique ID and optionally set custom properties.

```javascript
Astrolytics.identify('04f8846d-ecca-4a81-8740-f6428ceb7f7b', { firstName: 'Jordan', lastName: 'Walke' });
```

### Screen Tracking

Track screen views with the screen name and optional parameters.

```javascript
Astrolytics.page('/about', { foo: 'baz' });
```

### Disabling Tracking

To disable tracking

```javascript
Astrolytics.disableTracking();
```

### Enabling Tracking

To enable tracking

```javascript
Astrolytics.enableTracking();
```

## How to Contribute

We're always looking for contributions from the community. Here's how you can help:

1. **Report Bugs**: Create an issue report detailing the bug you've found.
2. **Suggest Features**: Have a great idea for Astrolytics? Don't hesitate to put it forward by creating an issue.
3. **Submit Pull Requests**: Feel free to fix a bug or add a new feature and create a pull request. Make sure to follow the existing code style, and write clear commit messages explaining your changes.
