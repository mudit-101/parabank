# Instructions

- Following Playwright test failed.
- Explain why, be concise, respect Playwright best practices.
- Provide a snippet of code with the fix, if possible.

# Test info

- Name: ui\InvalidLogin.spec.ts >> FR-09 Invalid Login
- Location: tests\ui\InvalidLogin.spec.ts:4:5

# Error details

```
Error: expect(locator).toContainText(expected) failed

Locator: locator('.error')
Expected substring: "The username and password could not be verified."
Received string:    "An internal error has occurred and has been logged."
Timeout: 5000ms

Call log:
  - Expect "toContainText" with timeout 5000ms
  - waiting for locator('.error')
    13 × locator resolved to <p class="error">An internal error has occurred and has been logge…</p>
       - unexpected value "An internal error has occurred and has been logged."

```

```yaml
- paragraph: An internal error has occurred and has been logged.
```

# Test source

```ts
  1  | import { test, expect } from '@playwright/test';
  2  | import { LoginPage } from '../../pages/LoginPage';
  3  | import loginData from '../../utils/loginData.json';
  4  | test('FR-09 Invalid Login', async ({page}) => {
  5  |     const loginPage = new LoginPage(page);
  6  |     await loginPage.navigateToLoginPage();
  7  |     await loginPage.login(
  8  |         loginData.invalidUser.username,
  9  |         loginData.invalidUser.password
  10 |     );
> 11 |     await expect(page.locator('.error')).toContainText('The username and password could not be verified.');
     |                                          ^ Error: expect(locator).toContainText(expected) failed
  12 | });
```