vanillabknd-sdk
===
[![npm version](https://img.shields.io/npm/v/vanillabknd-sdk.svg?style=flat-square)](https://www.npmjs.org/package/vanillabknd-sdk)
[![npm downloads](https://img.shields.io/npm/dt/vanillabknd-sdk.svg?style=flat-square)](http://npm-stat.com/charts.html?package=vanillabknd-sdk)

>  Backand SDK for JavaScript.
This SDK enables you to communicate comfortably and quickly with your Backand app.
It requires zero configurations, no installations and no requirements.


## Installation
- NPM:
```bash
$ npm i -S vanillabknd-sdk
```
```javascript
import backand from 'vanillabknd-sdk'
```
- CDN:
``` html
<script src="https://cdn.backand.net/javascript/dist/1.0.1/backand.min.js"></script>
```
- Download/Clone this repo and include `backand.min.js` in your project
``` html
<script src="backand.min.js"></script>
```


## Browser Support

![Chrome](https://raw.github.com/alrra/browser-logos/master/src/chrome/chrome_48x48.png) | ![Firefox](https://raw.github.com/alrra/browser-logos/master/src/firefox/firefox_48x48.png) | ![Safari](https://raw.github.com/alrra/browser-logos/master/src/safari/safari_48x48.png) | ![Opera](https://raw.github.com/alrra/browser-logos/master/src/opera/opera_48x48.png) | ![Edge](https://raw.github.com/alrra/browser-logos/master/src/edge/edge_48x48.png) | ![IE](https://raw.github.com/alrra/browser-logos/master/src/archive/internet-explorer_9-11/internet-explorer_9-11_48x48.png) |
--- | --- | --- | --- | --- | --- |
Latest ✔ | Latest ✔ | Latest ✔ | Latest ✔ | Latest ✔ | 10+ ✔ |


## Quick start
```javascript
backand.initiate({
  appName: 'APP_NAME',
  signUpToken: 'SIGNUP_TOKEN',
  anonymousToken: 'ANONYMOUS_TOKEN'
});

backand.service.useAnonymousAuth()
  .then(() => {
      return backand.service.getList('USERS');
  })
  .then((response) => {
      console.log(response);
  })
  .catch(function(error){
      console.log(error);
  });

```


## API

### backand namespace `window.backand`
The entry point to the sdk functions.

#### backand.initiate():
Creates a new backand instance.
```javascript
backand.initiate(config);
```
config:
- **appName** - Sets the name of your backand app (String) *required*
- **anonymousToken** - Sets the anonymous token of your backand app (String) *required*
- **signUpToken** - Sets the signup token of your backand app (String) *required*
- **apiUrl** - Sets the API url of backand servers (String) (Default: 'https://api.backand.com') *optional*
- **storagePrefix** - Sets prefix to use at the storage (String) (Default: 'BACKAND_') *optional*
- **storageType** - Sets the storage type to use (local/session) (String) (Default: 'local') *optional*
- **manageRefreshToken** - Determines whether the sdk should manage refresh tokens internally (Boolean) (Default: true) *optional*
- **runSigninAfterSignup** - Determines whether the sdk should run signin after signup automatically (Boolean) (Default: true) *optional*
- **runSocket** - Determines whether the sdk should run socket automatically (socketio-client required) (Boolean) (Default: false) *optional*
- **socketUrl** - Sets the socket url of backand servers (String) (Default: 'https://socket.backand.com') *optional*
- **isMobile** - Determines whether the sdk run on mobile platform (Boolean) (Default: false) *optional*

#### Properties:
| Name                     | Description                                              |
|--------------------------|----------------------------------------------------------|
| service                  | entry point to the sdk service functions                 |
| constants                | entry point to the sdk constants (EVENTS, URLS, SOCIALS) |
| helpers                  | entry point to the sdk helpers (filter, sort, exclude)   |
| socket (runSocket: true) | entry point to the sdk socket functions (on)             |

#### Methods backand.service:
##### auth:
| Name                                                                                 | Syntax                                                                                                                          |
|--------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------|
| useAnonymousAuth (scb)                                                               | backand.service.useAnonymousAuth(data=>{})                                                                                      |
| signin (username, password, scb, ecb)                                                | backand.service.signin(username, password, data=>{}, error=>{})                                                                 |
| signup (email, password, confirmPassword, firstName, lastName, parameters, scb, ecb) | backand.service.signin(email, password, confirmPassword, firstName, lastName, parameters, data=>{}, error=>{})                  |
| socialSignin (provider, scb, ecb, spec)                                              | backand.service.socialSignin(backand.constants.SOCIAL_PROVIDERS[provider].name, data=>{}, error=>{}, window.open - spec)        |
| socialSignup (provider, email, scb, ecb, spec)                                       | backand.service.socialSignup(backand.constants.SOCIAL_PROVIDERS[provider].name, email, data=>{}, error=>{}, window.open - spec) |
| requestResetPassword (username, scb, ecb)                                            | backand.service.requestResetPassword(username, data=>{}, error=>{})                                                             |
| resetPassword (newPassword, resetToken, scb, ecb)                                    | backand.service.resetPassword(newPassword, resetToken, data=>{}, error=>{})                                                     |
| changePassword (oldPassword, newPassword, scb, ecb)                                  | backand.service.changePassword(oldPassword, newPassword, data=>{}, error=>{})                                                   |
| signout (scb)                                                                        | backand.service.signout(data=>{})                                                                                               |
| getUserDetails(scb, ecb)                                                             | backand.service.getUserDetails(data=>{}, error=>{})                                                                             |
##### crud:
| Name                                        | Syntax                                                                |
|---------------------------------------------|-----------------------------------------------------------------------|
| getList (object, params, scb, ecb)          | backand.service.getList(object, params, data=>{}, error=>{})          |
| create (object, data, params, scb, ecb)     | backand.service.create(object, data, params, data=>{}, error=>{})     |
| getOne (object, id, params, scb, ecb)       | backand.service.getOne(object, id, params, data=>{}, error=>{})       |
| update (object, id, data, params, scb, ecb) | backand.service.update(object, id, data, params, data=>{}, error=>{}) |
| remove (object, id, scb, ecb)               | backand.service.remove(object, id, data=>{}, error=>{})               |
##### files:
| Name                                                          | Syntax                                                                                  |
|---------------------------------------------------------------|-----------------------------------------------------------------------------------------|
| uploadFile (object, fileAction, filename, filedata, scb, ecb) | backand.service.uploadFile(object, fileAction, filename, filedata, data=>{}, error=>{}) |
| deleteFile (object, fileAction, filename, scb, ecb)           | backand.service.getList(object, fileAction, filename, data=>{}, error=>{})              |
#### Methods backand.helpers:
| Name                                        | Syntax                                                                             |
|---------------------------------------------|------------------------------------------------------------------------------------|
| filter: create (fieldName, operator, value) | backand.helpers.filter.create(fieldName, backand.helpers.filter.operators, value); |
| sort: create (fieldName, order)             | backand.helpers.sort.create(fieldName, backand.helpers.sort.orders)                |
#### Methods backand.socket:
| Name              | Syntax                                 |
|-------------------|----------------------------------------|
| on(eventName, cb) | backand.socket.on(eventName, data=>{}) |

**NOTE:**
- **scb == Success Callback, ecb == Error Callback**
- **All Methods return Promise -> .then() .catch() are available**

#### Events:
| Name    | Description           | Syntax                                                                     |
|---------|-----------------------|----------------------------------------------------------------------------|
| SIGNIN  | dispatched on signin  | window.addEventListener(backand.constants.EVENTS.SIGNIN, (e)=>{}, false);  |
| SIGNOUT | dispatched on signout | window.addEventListener(backand.constants.EVENTS.SIGNOUT, (e)=>{}, false); |
| SIGNUP  | dispatched on signup  | window.addEventListener(backand.constants.EVENTS.SIGNUP, (e)=>{}, false);  |


## Examples
***To view the demo web page, just run npm start - [example page](https://github.com/backand/vanillabknd-sdk/blob/master/example/).***


## License

  [MIT](LICENSE)
