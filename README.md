# Debugging Notes

A compilation of errors you might see during Week 16 of App Academy's Online SWE
bootcamp.

## Chrome Debugger

To use the Chrome debugger:

* Add a `debugger` in the code that you're trying to hit, like a thunk or a
    reducer to make sure that you're updating state correctly
* Open the browser console
* Trigger the function. Depending on when your thunk is dispatched, it could be
    triggered when you reload the page or click a button
* Your app should pause when it hits the debugger and you can inspect variables
    in your Chrome DevTools
* You may step through or continue using the debugger menu bar

For more information, check out this page: [JavaScript Debugger].

## `Route Not Found` errors

If you're getting a `404` error where you can't get to a route, and you see the
error message in your browser console, there are a number of possibilities
depending on what you've done to get to this error message.

* If this is coming from navigation on the frontend of your application,
    consider checking the routes that are set up in the frontend to make sure
    that you've created the route with a path that matches where you're trying
    to go.
* It's possibly a thunk that is doing a `fetch` call to an API route that might
    1) not exist yet or
    2) might not have been attached to the backend app via
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

## `.findByPk` query doesn't return a row

If they're getting the `id` that they're using to query with from `req.params`,
check to see if they've converted that value to a Number type before querying
with it.

## Missing Re-render from a State Change

If the Redux DevTools are showing that something did change in the `Diff` tab,
and that an action did get dispatched, but the component in question did not
re-render to show the updated data, then there's probably something wrong with
the reducer case for this action type. Make sure that no accidental mutation of
the old state is happening, which might be a result of having a deeply nested
state object.

## Nothing seems to happen after a dispatch

Normally, I would say check for error messages, either in the browser console,
or in the backend terminal. But if nothing seems to be happening, then check the
backend route in question to see if they are sending any kind of response after
the request has been completed. Some of the time, they just need to `res.json()`
something, even an empty object would help. This lets the `fetch` in the
frontend continue (and potentially show whatever errors were actually there).

## `.map` is not a function

Since it's getting to the `.map` call without error-ing out, we know that the
variable that you're calling the `.map` method on is not `undefined`, which is
good. But we also know that it's not an `Array` since we can't call the `.map`
method on it.

## `431: Request Headers too large`

Usually happens when the React frontend tries to proxy requests to itself. Check
the `frontend/package.json` to see what the `"proxy"` key is, and make sure that
it is pointing to the backend development server. You'll need to restart the
frontend server if you've made a change to the `package.json`.

[JavaScript Debugger]: https://javascript.info/debugging-chrome

## Sequelize: TypeError: Cannot read property `replace` of undefined

Typically seen when Sequelize is attempting to read a variable taken from the
environment (like a `.env` file through the `dotenv` command). If the
environment variables are unavailable, then Sequelize will end up attempting to
call the `replace` method on `undefined`.

You can check for the existence of the environment variables that are being used
by placing a `console.log(config)` near the top of the `config/database.js`
file to examine the `config` object imported from the `config/index.js` file.

Sometimes, the student has just forgotten the `dotenv` part of the `db:`
commands. Sometimes, it might be a little more than that.
