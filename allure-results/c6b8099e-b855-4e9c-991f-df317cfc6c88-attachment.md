# Instructions

- Following Playwright test failed.
- Explain why, be concise, respect Playwright best practices.
- Provide a snippet of code with the fix, if possible.

# Test info

- Name: e2e\CreateAccAndValidate.spec.ts >> Hybrid Scenario - Create Account and Validate API
- Location: tests\e2e\CreateAccAndValidate.spec.ts:8:5

# Error details

```
Error: locator.click: Target page, context or browser has been closed
Call log:
  - waiting for locator('input[value="Log In"]')
    - locator resolved to <input type="submit" class="button" value="Log In"/>
  - attempting click action
    - waiting for element to be visible, enabled and stable

```

# Test source

```ts
  1  | import { Page } from '@playwright/test';
  2  | 
  3  | export class LoginPage {
  4  | 
  5  |     constructor(private page: Page) {}
  6  | 
  7  |     async navigateToLoginPage() {
  8  |         await this.page.goto(
  9  |             'https://parabank.parasoft.com/parabank/index.htm'
  10 |         );
  11 |     }
  12 | 
  13 |     async login(username: string, password: string) {
  14 | 
  15 |         await this.page.locator('input[name="username"]').fill(username);
  16 | 
  17 |         await this.page.locator('input[name="password"]').fill(password);
  18 | 
> 19 |         await this.page.locator('input[value="Log In"]').click();
     |                                                          ^ Error: locator.click: Target page, context or browser has been closed
  20 |     }
  21 | }
```