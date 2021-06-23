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
