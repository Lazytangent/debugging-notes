# Debugging Notes

A compilation of errors you might see during Week 16 of App Academy's Online SWE
bootcamp.

The notes are split up by section to (hopefully) make finding the issue you're
having easier.

* [General][general]
* [React and Redux][react-redux]
* [Error Codes][error-codes]
* [Sequelize][sequelize]

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

[JavaScript Debugger]: https://javascript.info/debugging-chrome

[general]: ./GENERAL.md
[react-redux]: ./REACT_REDUX.md
[error-codes]: ./ERROR_CODES.md
[sequelize]: ./SEQUELIZE.md
