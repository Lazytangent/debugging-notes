# Error Codes

A collection of common error/status codes.

## Error Code: 403

This typically means that the student is NOT using the `csrfFetch` from the
Authenticate Me Walkthrough, but is instead using the `fetch` API.

If not the first thing, then it's possible that their CSRF is not correctly set
up, either in their `csrfFetch` or in their backend `app.js` or
`routes/index.js`

## `404: Route Not Found` errors

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

## `431: Request Headers too large`

Usually happens when the React frontend tries to proxy requests to itself. Check
the `frontend/package.json` to see what the `"proxy"` key is, and make sure that
it is pointing to the backend development server. You'll need to restart the
frontend server if you've made a change to the `package.json`.

## Error Code: 500

You'll have to look in their backend terminal for this. If it is a Sequelize
error, it'll be really long. Look for the part that says something about
`original: error: ...` That should normally point you to where things are
breaking.
