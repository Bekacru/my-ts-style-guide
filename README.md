# Style guide

## General
- Use tabs (4 spaces)
- Use interfaces for Main/Parent types and type for sub types, functions and generics.
```ts 
// bad
interface Login {
    (username: string, password: string) => Promise<void>;
}
type Action = {
    login: Login
}

//good
type Login = (username: string, password: string) => Promise<void>;
interface Action {
    login: Login
}
```
- Use `"` instead of `'`.
- Use `const` when possible.
- Avoid mutability.
- Avoid using `var`.
- Avoid using classes. Unless you are required to.
- `await` instead of `.then`.
- Separate type and regular imports.

  ```ts
  // bad
  import { someFunction, SomeType } from "foo";
  import { someFunction, type SomeType } from "foo";

  // good
  import { someFunction } from "foo";
  import type { SomeType } from "foo";
  ```

## Naming convention

- Use camelCase for variables and functions, and SCREAMING_SNAKE_CASE for constants.
  ```ts
  let foo = 0;
  let fooBar = 0;
  const CONSTANT_VALUES_FOR_ALGORITHM = [1, 1, 1] as const;
  ```
- Use PascalCase case for types, interfaces, and classes.
  ```ts
  interface FooBar {
    a: string;
  }
  ```
- use kebab-case for files and folders.
- Variable names should not start with `is`, `has`, etc. Those should be limited to functions that return booleans.
- Avoid single letter variables.
- Acronyms should be in uppercase unless they're the first word in the name.

  ```ts
  function createHTTPServer(): void {
    // ...
  }

  let httpStatus: number;

  interface HTTPPOSTRequest {}
  ```

## Functions

- Use named functions instead of arrow functions for top-level function.

  ```ts
  // bad
  const foo = () => {};

  // good
  function foo() {}
  ```

- Try to infer types as much as possible.

  ```ts
  // bad
  function foo(a: number): number {
    return a;
    // ...
  }

  function foo(a: number) {
    return a;
    // ...
  }
  ```

- Functions should be strict in what values they accept and return. Do not use union types except for representing multiple string literals.

  ```ts
  // bad
  function foo(a: string | number): string | number {
    // ...
  }

  // good
  function foo(a: string): string {
    // ...
  }

  function foo(a: "a" | "b"): void {
    // ...
  }
  ```

- No object parameters unless specified otherwise.

  ```ts
  // bad
  function foo(args: { a: string; b: string }): void {
    // ...
  }

  // good
  function foo(a: string, b: string): void {
    // ...
  }
  ```

- No optional parameters except for a single `options` object parameter.

  ```ts
  // bad
  function foo(a?: string): void {
    // ...
  }

  // good
  function foo(options?: { a?: string }): void {
    // ...
  }
  ```

- Avoid callback functions unless necessary. Reconsider the API design.
  ```ts
  // avoid
  function foo(onEvent: () => void): void {
    // ...
  }
  ```
- Avoid boolean parameters. If necessary, it should be an optional property in the `options` parameter though you should reconsider the API design.

  ```ts
  // bad
  function foo(a: boolean): void {
    // ...
  }

  // bad but better
  function foo(options?: { a?: boolean }): void {
    // ...
  }
  ```

- Return errors if they should be handled by the caller. Only throw if it's unexpected.


## Control flow

### If statements

- Use `{}`.

  ```ts
  // bad
  if (condition) stuff;

  // good
  if (condition) {
    stuff;
  }
  ```

- Use shortcuts only for booleans.

  ```ts
  // bad
  if (thisIsABoolean === true) {
    // ...
  }
  if (thisIsAString) {
    // ...
  }

  // good
  if (thisIsABoolean) {
    // ...
  }
  if (thisIsAString !== "") {
    // ...
  }
  ```

- Never use `==` or `!=`.

### Other

- Embrace simple `for` loops. Don't try to force `.map()` and don't use `.forEach()`.
- Avoid `finally`.
