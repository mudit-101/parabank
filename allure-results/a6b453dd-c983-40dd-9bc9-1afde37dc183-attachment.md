# Instructions

- Following Playwright test failed.
- Explain why, be concise, respect Playwright best practices.
- Provide a snippet of code with the fix, if possible.

# Test info

- Name: e2e\TransferAndValidate.spec.ts >> scen-7 and scen-8 validate transfer money
- Location: tests\e2e\TransferAndValidate.spec.ts:7:5

# Error details

```
Error: page.waitForFunction: Target page, context or browser has been closed
```

# Test source

```ts
  1  | import { Page, expect } from '@playwright/test';
  2  | 
  3  | export class TransferFundsPage {
  4  |     constructor(private page: Page) {}
  5  |     async navigateToTransferFundsPage() {
  6  |         await this.page.getByRole('link', {name: 'Transfer Funds'}).click();
  7  |         await expect(this.page.getByRole('heading', {name: 'Transfer Funds'})).toBeVisible();
  8  |     }
  9  |     async getSelectedAccounts() {
> 10 |         await this.page.waitForFunction(() => {
     |                         ^ Error: page.waitForFunction: Target page, context or browser has been closed
  11 |             return document.querySelectorAll(
  12 |                 '#fromAccountId option'
  13 |             ).length > 1;
  14 |         });
  15 |         const accounts = await this.page
  16 |             .locator('#fromAccountId option')
  17 |             .evaluateAll(options =>
  18 |                 options.map(
  19 |                     option =>
  20 |                         (option as HTMLOptionElement).value
  21 |                 )
  22 |             );
  23 |         console.log('Available Accounts:',accounts);
  24 |         return {
  25 |             fromAccount: accounts[0],
  26 |             toAccount: accounts[1]
  27 |         };
  28 |     }
  29 |     async transferFunds(
  30 |         amount: string,
  31 |         fromAccount: string,
  32 |         toAccount: string
  33 |     ) {
  34 |         await this.page.locator('#amount').fill(amount);
  35 |         await this.page.locator('#fromAccountId').selectOption(fromAccount);
  36 |         await this.page.locator('#toAccountId').selectOption(toAccount);
  37 |         console.log(`From Account: ${fromAccount}`);
  38 |         console.log(`To Account: ${toAccount}`);
  39 |         await this.page.locator('input[value="Transfer"]').click();
  40 |         console.log(`Transferred Amount: ${amount}`);
  41 |     }
  42 |     async verifyTransferCompleted() {
  43 |         await this.page.waitForLoadState('networkidle');
  44 |         await expect(this.page.locator('#showResult')).toContainText('Transfer Complete');
  45 |         console.log('Transfer completed successfully');
  46 |         await this.page.screenshot({path: 'screenshots/transfer-completed.png',fullPage: true});
  47 |     }
  48 | }
```