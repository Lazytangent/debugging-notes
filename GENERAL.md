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
