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
  - waiting for getByRole('link', { name: 'Open New Account' })

```

# Test source

```ts
  1  | import { Page, expect } from '@playwright/test';
  2  | 
  3  | export class OpenAccountPage {
  4  | 
  5  |     constructor(private page: Page) {}
  6  | 
  7  |     async navigateToOpenAccountPage() {
  8  | 
  9  |         await this.page.getByRole('link', {
  10 |             name: 'Open New Account'
> 11 |         }).click();
     |            ^ Error: locator.click: Target page, context or browser has been closed
  12 | 
  13 |         await expect(
  14 |             this.page.getByRole('heading', {
  15 |                 name: 'Open New Account'
  16 |             })
  17 |         ).toBeVisible();
  18 |     }
  19 | 
  20 |     async selectAccountType(type: string) {
  21 | 
  22 |         await this.page.selectOption(
  23 |             '#type',
  24 |             type
  25 |         );
  26 |     }
  27 | 
  28 |     async clickOpenNewAccount() {
  29 | 
  30 |         await this.page.locator(
  31 |             'input[value="Open New Account"]'
  32 |         ).click();
  33 |     }
  34 | 
  35 |     async createNewAccount(type: string) {
  36 | 
  37 |         await this.navigateToOpenAccountPage();
  38 | 
  39 |         await this.selectAccountType(type);
  40 | 
  41 |         await this.clickOpenNewAccount();
  42 |     }
  43 | 
  44 |     async verifyAccountCreated() {
  45 | 
  46 |         await this.page.waitForLoadState('networkidle');
  47 | 
  48 |         const accountId = await this.page
  49 |             .locator('#newAccountId')
  50 |             .textContent();
  51 | 
  52 |         console.log(
  53 |             'New Account Created:',
  54 |             accountId
  55 |         );
  56 | 
  57 |         expect(
  58 |             accountId?.trim().length
  59 |         ).toBeGreaterThan(0);
  60 | 
  61 |         await this.page.screenshot({
  62 |             path: 'screenshots/account-created.png',
  63 |             fullPage: true
  64 |         });
  65 | 
  66 |         return accountId?.trim();
  67 |     }
  68 | 
  69 |     async getAccountNumber() {
  70 | 
  71 |         const accountNumber = await this.page
  72 |             .locator('#newAccountId')
  73 |             .textContent();
  74 | 
  75 |         return accountNumber?.trim();
  76 |     }
  77 | }
```