# Instructions

- Following Playwright test failed.
- Explain why, be concise, respect Playwright best practices.
- Provide a snippet of code with the fix, if possible.

# Test info

- Name: ui\CreateAccount.spec.ts >> scen -2 Create new acc
- Location: tests\ui\CreateAccount.spec.ts:5:5

# Error details

```
Error: page.goto: Target page, context or browser has been closed
```

# Test source

```ts
  1  | import { Page } from '@playwright/test';
  2  | 
  3  | export class LoginPage {
  4  |     constructor(private page: Page) {}
  5  |     async navigateToLoginPage() {
> 6  |         await this.page.goto(
     |                         ^ Error: page.goto: Target page, context or browser has been closed
  7  |             'https://parabank.parasoft.com/parabank/index.htm'
  8  |         );
  9  |     }
  10 |     async login(username: string, password: string) {
  11 |         await this.page.locator('input[name="username"]').fill(username);
  12 |         await this.page.locator('input[name="password"]').fill(password);
  13 |         await this.page.locator('input[value="Log In"]').click();
  14 |     }
  15 | }
```