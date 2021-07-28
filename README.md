# Debugging Notes

A compilation of errors you might see during Week 16 of App Academy's Online SWE
bootcamp.

## `Route Not Found` errors

If you're getting a `404` error where you can't get to a route, and you see the
error message in your browser console, there are a number of possibilities
depending on what you've done to get to this error message.

* If this is coming from navigation on the frontend of your application,
    consider checking the routes that are set up in the frontend to make sure
    that you've created the route with a path that matches where you're trying
    to go.
* It's possibly a thunk that is doing a `fetch` call to an API route that might
    1) not exist yet or 2) might not have been attached to the backend app via
    `router.use` and `app.use`.

## Error Code: 403

This typically means that the student is NOT using the `csrfFetch` from the
Authenticate Me Walkthrough, but is instead using the `fetch` API.

If not the first thing, then it's possible that their CSRF is not correctly set
up, either in their `csrfFetch` or in their backend `app.js` or
`routes/index.js`

## `token` cookie gets removed on when `restoreUser` middleware is used

Check the `restoreUser` middleware function and make sure that it's actually
checking for a `user` object on the request (`req`).

## Error Code: 500

You'll have to look in their backend terminal for this. If it is a Sequelize
error, it'll be really long. Look for the part that says something about
`original: error: ...` That should normally point you to where things are
breaking.

### Something about a column not existing

Check the associations for a column name that doesn't exist on the right model.

* Foreign keys on a `belongsTo` should exist on the current model.
* Foreign keys on a `hasOne` or `hasMany` should exist on the opposing model.

Occasionally, you might find a typo on a column name.

## `Object(...)` is not a function

Or the occasional `console.log(...)` is not a function.

Usually seen when an IIFE is used after a line that doesn't end with a
semicolon.

## `update or delete ... violates constraints`

Check the associations. If they have the `onDelete: 'cascade', hooks: true`
portion in their association object, remember that the individual hook only
fires when the instance method version of `.destroy()` or `.update()` is used.
They can query with a `.findByPk()` to get the row to destroy or update, and
call the instance method on that instance.

Make sure that the `onDelete: 'cascade', hooks: true` settings are only on the
association object on one side if the association. If you have them on both
sides, you'll cause recursive loops of SQL queries.

## Params are returning undefined

Check the route path to make sure that the wildcard set matches the variable
getting pulled from the params. This applies to both frontend `Route` components
and backend Express routes.
