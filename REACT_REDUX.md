# React Redux Issues

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
