# Instructions

- Following Playwright test failed.
- Explain why, be concise, respect Playwright best practices.
- Provide a snippet of code with the fix, if possible.

# Test info

- Name: e2e\TransferAndValidate.spec.ts >> FR-06 & FR-07 Transfer Funds and Validate Balance
- Location: tests\e2e\TransferAndValidate.spec.ts:6:5

# Error details

```
Error: locator.selectOption: Target page, context or browser has been closed
Call log:
  - waiting for locator('#fromAccountId')
    - locator resolved to <select class="input" id="fromAccountId"></select>
  - attempting select option action
    2 × waiting for element to be visible and enabled
      - did not find some options
    - retrying select option action
    - waiting 20ms
    2 × waiting for element to be visible and enabled
      - did not find some options
    - retrying select option action
      - waiting 100ms
    34 × waiting for element to be visible and enabled
       - did not find some options
     - retrying select option action
       - waiting 500ms

```

# Test source

```ts
  1  | import { Page, expect } from '@playwright/test';
  2  | 
  3  | export class TransferFundsPage {
  4  | 
  5  |     constructor(private page: Page) {}
  6  | 
  7  |     async navigateToTransferFundsPage() {
  8  |         await this.page.getByRole('link', { name: 'Transfer Funds'}).click();
  9  | 
  10 |         await expect(this.page.getByRole('heading', { name: 'Transfer Funds'})).toBeVisible();
  11 |     }
  12 | 
  13 |   async transferFunds(amount: string) {
  14 | 
  15 |     await this.page.locator('#amount').fill(amount);
  16 | 
  17 |     // Wait for dropdowns
  18 |     await this.page.locator('#fromAccountId').waitFor();
  19 | 
  20 |     await this.page.locator('#toAccountId').waitFor();
  21 | 
  22 |     const fromOptions =await this.page.locator('#fromAccountId option').count();
  23 | 
  24 |     const toOptions =await this.page.locator('#toAccountId option').count();
  25 | 
> 26 |     await this.page.locator('#fromAccountId').selectOption('13677');
     |                                               ^ Error: locator.selectOption: Target page, context or browser has been closed
  27 | 
  28 |     if (toOptions > 1) {
  29 | 
  30 |         await this.page.locator('#toAccountId').selectOption('13677');
  31 |     } else {
  32 | 
  33 |         await this.page.locator('#toAccountId') .selectOption({ index: 0 });
  34 | 
  35 |     }
  36 | 
  37 |     const fromAccount =
  38 |         await this.page.locator('#fromAccountId') .inputValue();
  39 | 
  40 |     const toAccount =
  41 |         await this.page.locator('#toAccountId') .inputValue();
  42 | 
  43 |     console.log('From Account:', fromAccount);
  44 |     console.log('To Account:', toAccount);
  45 | 
  46 |     await this.page.locator('input[value="Transfer"]' ).click();
  47 | 
  48 |     console.log(`Transferred Amount: ${amount}`);
  49 | }
  50 | 
  51 |    async verifyTransferCompleted() {
  52 | 
  53 |     await this.page.waitForLoadState('networkidle');
  54 | 
  55 |     await expect(
  56 |     this.page.locator('#showResult')
  57 |    ).toContainText('Transfer Complete');
  58 | 
  59 |     console.log(
  60 |     'Transfer completed successfully'
  61 |      );
  62 | 
  63 |     await this.page.screenshot({
  64 |         path: 'screenshots/transfer-completed.png',
  65 |         fullPage: true
  66 |     });
  67 | }
  68 | }
```