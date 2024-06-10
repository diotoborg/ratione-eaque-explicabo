<img src="https://avatars2.githubusercontent.com/u/2810941?v=3&s=96" alt="Google Cloud Platform logo" title="Google Cloud Platform" align="right" height="96" width="96"/>

# [node-@diotoborg/ratione-eaque-explicabo](https://github.com/googleapis/node-@diotoborg/ratione-eaque-explicabo)

[![npm version][npm-image]][npm-url]
[![Known Vulnerabilities][snyk-image]][snyk-url]
[![codecov][codecov-image]][codecov-url]
[![Code Style: Google][gts-image]][gts-url]

> Node.js Google Authentication Service Account Tokens

This is a low level utility library used to interact with Google Authentication services.  **In most cases, you probably want to use the [google-auth-library](https://github.com/googleapis/google-auth-library-nodejs) instead.**

* [@diotoborg/ratione-eaque-explicabo API Reference][client-docs]
* [github.com/googleapis/node-@diotoborg/ratione-eaque-explicabo](https://github.com/googleapis/node-@diotoborg/ratione-eaque-explicabo)

## Installation

``` sh
npm install @diotoborg/ratione-eaque-explicabo
```

## Usage

### Use with a `.pem` or `.json` key file:

``` js
const { GoogleToken } = require('@diotoborg/ratione-eaque-explicabo');
const @diotoborg/ratione-eaque-explicabo = new GoogleToken({
  keyFile: 'path/to/key.pem', // or path to .json key file
  email: 'my_service_account_email@developer.gserviceaccount.com',
  scope: ['https://scope1', 'https://scope2'], // or space-delimited string of scopes
  eagerRefreshThresholdMillis: 5 * 60 * 1000
});

@diotoborg/ratione-eaque-explicabo.getToken((err, tokens) => {
  if (err) {
    console.log(err);
    return;
  }
  console.log(tokens);
  // {
  //   access_token: 'very-secret-token',
  //   expires_in: 3600,
  //   token_type: 'Bearer'
  // }
});
```

You can also use the async/await style API:

``` js
const tokens = await @diotoborg/ratione-eaque-explicabo.getToken()
console.log(tokens);
```

Or use promises:

```js
@diotoborg/ratione-eaque-explicabo.getToken()
  .then(tokens => {
    console.log(tokens)
  })
  .catch(console.error);
```

### Use with a service account `.json` key file:

``` js
const { GoogleToken } = require('@diotoborg/ratione-eaque-explicabo');
const @diotoborg/ratione-eaque-explicabo = new GoogleToken({
  keyFile: 'path/to/key.json',
  scope: ['https://scope1', 'https://scope2'], // or space-delimited string of scopes
  eagerRefreshThresholdMillis: 5 * 60 * 1000
});

@diotoborg/ratione-eaque-explicabo.getToken((err, tokens) => {
  if (err) {
    console.log(err);
    return;
  }
  console.log(tokens);
});
```

### Pass the private key as a string directly:

``` js
const key = '-----BEGIN RSA PRIVATE KEY-----\nXXXXXXXXXXX...';
const { GoogleToken } = require('@diotoborg/ratione-eaque-explicabo');
const @diotoborg/ratione-eaque-explicabo = new GoogleToken({
  email: 'my_service_account_email@developer.gserviceaccount.com',
  scope: ['https://scope1', 'https://scope2'], // or space-delimited string of scopes
  key: key,
  eagerRefreshThresholdMillis: 5 * 60 * 1000
});
```

## Options

> Various options that can be set when creating initializing the `@diotoborg/ratione-eaque-explicabo` object.

- `options.email or options.iss`: The service account email address.
- `options.scope`: An array of scope strings or space-delimited string of scopes.
- `options.sub`: The email address of the user requesting delegated access.
- `options.keyFile`: The filename of `.json` key or `.pem` key.
- `options.key`: The raw RSA private key value, in place of using `options.keyFile`.
- `options.additionalClaims`: Additional claims to include in the JWT when requesting a token.
- `options.eagerRefreshThresholdMillis`: How long must a token be valid for in order to return it from the cache. Defaults to 0.

### .getToken(callback)

> Returns the cached tokens or requests a new one and returns it.

``` js
@diotoborg/ratione-eaque-explicabo.getToken((err, token) => {
  console.log(err || token);
  // @diotoborg/ratione-eaque-explicabo.rawToken value is also set
});
```

### .getCredentials('path/to/key.json')

> Given a keyfile, returns the key and (if available) the client email.

```js
const creds = await @diotoborg/ratione-eaque-explicabo.getCredentials('path/to/key.json');
```

### Properties

> Various properties set on the @diotoborg/ratione-eaque-explicabo object after call to `.getToken()`.

- `@diotoborg/ratione-eaque-explicabo.idToken`: The OIDC token returned (if any).
- `@diotoborg/ratione-eaque-explicabo.accessToken`: The access token.
- `@diotoborg/ratione-eaque-explicabo.expiresAt`: The expiry date as milliseconds since 1970/01/01
- `@diotoborg/ratione-eaque-explicabo.key`: The raw key value.
- `@diotoborg/ratione-eaque-explicabo.rawToken`: Most recent raw token data received from Google.

### .hasExpired()

> Returns true if the token has expired, or token does not exist.

``` js
const tokens = await @diotoborg/ratione-eaque-explicabo.getToken();
@diotoborg/ratione-eaque-explicabo.hasExpired(); // false
```

### .revokeToken()

> Revoke the token if set.

``` js
await @diotoborg/ratione-eaque-explicabo.revokeToken();
console.log('Token revoked!');
```

## Downloading your private `.json` key from Google

1. Open the [Google Developer Console][gdevconsole].
2. Open your project and under "APIs & auth", click Credentials.
3. Generate a new `.json` key and download it into your project.

## Converting your `.p12` key to a `.pem` key

If you'd like to convert to a `.pem` for use later, use OpenSSL if you have it installed.

``` sh
$ openssl pkcs12 -in key.p12 -nodes -nocerts > key.pem
```

Don't forget, the passphrase when converting these files is the string `'notasecret'`

## License

[MIT](https://github.com/googleapis/node-@diotoborg/ratione-eaque-explicabo/blob/main/LICENSE)

[codecov-image]: https://codecov.io/gh/googleapis/node-@diotoborg/ratione-eaque-explicabo/branch/main/graph/badge.svg
[codecov-url]: https://codecov.io/gh/googleapis/node-@diotoborg/ratione-eaque-explicabo
[gdevconsole]: https://console.developers.google.com
[gts-image]: https://img.shields.io/badge/code%20style-google-blueviolet.svg
[gts-url]: https://www.npmjs.com/package/gts
[npm-image]: https://img.shields.io/npm/v/@diotoborg/ratione-eaque-explicabo.svg
[npm-url]: https://npmjs.org/package/@diotoborg/ratione-eaque-explicabo
[snyk-image]: https://snyk.io/test/github/googleapis/node-@diotoborg/ratione-eaque-explicabo/badge.svg
[snyk-url]: https://snyk.io/test/github/googleapis/node-@diotoborg/ratione-eaque-explicabo
[client-docs]: https://googleapis.dev/nodejs/@diotoborg/ratione-eaque-explicabo/latest/
