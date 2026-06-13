# Instructions

- Following Playwright test failed.
- Explain why, be concise, respect Playwright best practices.
- Provide a snippet of code with the fix, if possible.

# Test info

- Name: ui\AccountOverview.spec.ts >> FR-06 Account Overview Validation
- Location: tests\ui\AccountOverview.spec.ts:5:5

# Error details

```
Error: page.goto: Test ended.
Call log:
  - navigating to "https://parabank.parasoft.com/parabank/index.htm", waiting until "load"

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
> 8  |         await this.page.goto(
     |                         ^ Error: page.goto: Test ended.
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
  19 |         await this.page.locator('input[value="Log In"]').click();
  20 |     }
  21 | }
```