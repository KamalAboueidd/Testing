#  Testing — Fundamentals

## 1. What is Testing?

Testing means checking if our code works as we expect.

We write tests to make sure our code gives the correct results.

## 2. Important Testing Terms

### Test Case
A test case is one situation that we want to test.

### Expected Result
The expected result is the result we want to get.

### Actual Result
The actual result is the real result from our code.

### Assertion
An assertion checks if the actual result is equal to the expected result.

Example:

```js
expect(20).toBe(20);
```

The actual value is `20`, and the expected value is `20`.

The assertion passes because both values are equal.

## 3. The `test()` Function

We use `test()` to create one test case.

It takes two main arguments:

- A name that explains the test.
- A function that contains the test code.

Example:

```js
test("should multiply two numbers", () => {
  expect(4 * 5).toBe(20);
});
```

## 4. The `expect()` Function and `.toBe()`

We use `expect()` to give the actual value to the testing tool.

We use `.toBe()` to check if the actual value is equal to the expected value.

Example:

```js
expect(2 + 3).toBe(5);
```

- `2 + 3` is the actual value.
- `5` is the expected value.
- `.toBe(5)` checks if both values are equal.

## 5. PASS and FAIL

### PASS
A test passes when the actual result is equal to the expected result.

```js
expect(10).toBe(10);
```

Result: PASS.

### FAIL
A test fails when the actual result is different from the expected result.

```js
expect(10).toBe(20);
```

Result: FAIL.

A failing test does not always mean the function is broken. The expected value in the test may also be wrong.

## 6. The `describe()` Function

We use `describe()` to group related tests together.

This group is called a **Test Suite**.

We use `test()` inside `describe()` to create individual test cases.

Example:

```js
describe("Calculator Tests", () => {
  test("should add two numbers", () => {
    expect(2 + 3).toBe(5);
  });

  test("should multiply two numbers", () => {
    expect(4 * 5).toBe(20);
  });
});
```

In this example:

- `describe()` creates one Test Suite.
- The first `test()` checks addition.
- The second `test()` checks multiplication.
- Both tests belong to the same group.

## 7. AAA Pattern

AAA is a simple way to organize the steps inside a test.

AAA stands for:

### Arrange
Prepare everything we need for the test.

### Act
Run the function that we want to test.

### Assert
Check if the actual result is equal to the expected result.

Example:

```js
function multiply(a, b) {
  return a * b;
}

test("should multiply two numbers", () => {
  // Arrange
  const firstNumber = 4;
  const secondNumber = 5;

  // Act
  const result = multiply(firstNumber, secondNumber);

  // Assert
  expect(result).toBe(20);
});
```

### AAA Steps

1. Arrange: We prepare two numbers.
2. Act: We call the `multiply()` function.
3. Assert: We check if the result is `20`.

## 8. Practical Example: Testing User Roles

We have a function that returns a user role.

```js
function getUserRole(user) {
  return user.isAdmin ? "Admin" : "User";
}
```

We want to test both normal users and admin users.

```js
describe("User Role Tests", () => {

  test("should return User for a normal user", () => {
    // Arrange
    const user = { isAdmin: false };

    // Act
    const result = getUserRole(user);

    // Assert
    expect(result).toBe("User");
  });

  test("should return Admin for an admin user", () => {
    // Arrange
    const user = { isAdmin: true };

    // Act
    const result = getUserRole(user);

    // Assert
    expect(result).toBe("Admin");
  });

});
```

Each test checks a different situation.

Both tests should PASS.

## 9. Test Independence

Test Independence means each test can run alone.

A test should not need another test to run first.

Example of a problem:

```js
let user = null;

test("should create a user", () => {
  user = { name: "Ahmed" };

  expect(user.name).toBe("Ahmed");
});

test("should check user name", () => {
  expect(user.name).toBe("Ahmed");
});
```

The second test needs the first test to create the user.

If the second test runs alone, it fails because `user` is still `null`.

A better way is to prepare the user inside each test:

```js
test("should create a user", () => {
  const user = { name: "Ahmed" };

  expect(user.name).toBe("Ahmed");
});

test("should check user name", () => {
  const user = { name: "Ahmed" };

  expect(user.name).toBe("Ahmed");
});
```

Now, each test can run alone.

## 10. Test Isolation

Test Isolation means each test has its own data and does not affect the data of another test.

### Example of a problem

```js
let balance = 100;

test("should add money", () => {
  balance += 50;

  expect(balance).toBe(150);
});

test("should start with 100", () => {
  expect(balance).toBe(100);
});
```

What happens?

1. The first test changes `balance` from `100` to `150`.
2. The second test uses the same variable.
3. The actual value is now `150`, not `100`.
4. The second test fails if it runs after the first test.

### A better way

```js
test("should add money", () => {
  let balance = 100;

  balance += 50;

  expect(balance).toBe(150);
});

test("should start with 100", () => {
  let balance = 100;

  expect(balance).toBe(100);
});
```

Now, each test has its own `balance` variable.

Changing the value in the first test does not change the value in the second test.

Both tests PASS.

## 11. Test Independence vs Test Isolation

| Test Independence | Test Isolation |
|---|---|
| A test can run alone. | A test does not affect another test. |
| A test does not need another test. | A test has its own data and state. |
| Focuses on test dependencies. | Focuses on shared data and side effects. |

Both concepts help us write reliable tests.

## 12. Important Notes

- `test()`, `expect()`, and `describe()` are not built into JavaScript.
- Testing frameworks like Vitest and Jest provide these functions.
- A normal JavaScript compiler may not recognize them.
- We need a testing framework to run our tests.
- AAA helps us organize our test code.
- A Test Suite groups related test cases.
- Every test should be clear and easy to understand.

---

## Final Summary

Testing helps us check if our code works correctly.

We use:

- `test()` to create an individual test.
- `expect()` to provide the actual value.
- `.toBe()` to compare the actual and expected values.
- `describe()` to group related tests.
- AAA to organize test steps.
- Test Independence to make sure tests can run alone.
- Test Isolation to stop tests from affecting each other.

**Our next step: Start learning Vitest and write real tests in a JavaScript project.**

<img width="1786" height="878" alt="image" src="https://github.com/user-attachments/assets/20bde340-d7a0-44b9-b007-d7bb663ba3b6" />
<img width="1521" height="539" alt="image" src="https://github.com/user-attachments/assets/ca3fbb0e-821f-4118-80f5-84c012fdf467" />
<img width="1795" height="684" alt="image" src="https://github.com/user-attachments/assets/6590e144-d9b4-4fff-a277-2591d0cf2f23" />
<img width="1155" height="485" alt="image" src="https://github.com/user-attachments/assets/64309368-6fa6-43bb-8af6-c649ee2d64d8" />
<img width="1341" height="625" alt="image" src="https://github.com/user-attachments/assets/696b0a62-1a56-4f4d-934c-5f6bf56140cf" />
<img width="568" height="668" alt="image" src="https://github.com/user-attachments/assets/d8c27ac4-8007-497d-879c-4c698b34b1f5" />
<img width="754" height="844" alt="image" src="https://github.com/user-attachments/assets/d9ad43cc-8c18-41a5-b69d-16c6bebe9aab" />
<img width="444" height="573" alt="image" src="https://github.com/user-attachments/assets/8c014cdd-42a1-4be8-8532-865d0c720d3e" />




