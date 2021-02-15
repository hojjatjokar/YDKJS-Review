## 1. What's promise paradigm?

if instead of handing the continuation of our program to another party (Inversion of control), we could expect it to return us a capability to know when its task finishes, and then our code could decide what to do next. This paradigm is called promise.

## 2. What Is a Promise?

A promise is an object that may produce a single value some time in the future: either a resolved value, or a reason that it’s not resolved (e.g., a network error occurred). A promise may be in one of 3 possible states: fulfilled, rejected, or pending. Promise users can attach callbacks to handle the fulfilled value or the reason for rejection.

## 3.
