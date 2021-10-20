# General Errors and Issues

## `token` cookie gets removed on when `restoreUser` middleware is used

Check the `restoreUser` middleware function and make sure that it's actually
checking for a `user` object on the request (`req`).

## `Object(...)` is not a function

Or the occasional `console.log(...)` is not a function.

Usually seen when an IIFE is used after a line that doesn't end with a
semicolon.

## Params are returning undefined

Check the route path to make sure that the wildcard set matches the variable
getting pulled from the params. This applies to both frontend `Route` components
and backend Express routes.

## Testing with Postman - No body gets sent to backend

If you're testing routes that can take a request body with Postman and the
request body doesn't show up when you `console.log` it in the route handler,
then check the headers on the Postman request. Be sure to have all the headers
that Postman sets. You'll at least need the `Content-Type` and the
`Content-Length` headers for the request to be properly parsed in the backend.
