# Instructions

- Following Playwright test failed.
- Explain why, be concise, respect Playwright best practices.
- Provide a snippet of code with the fix, if possible.

# Test info

- Name: ui\TransferMessageValidation.spec.ts >> FR-08 Validate Transfer Success Message
- Location: tests\ui\TransferMessageValidation.spec.ts:5:5

# Error details

```
Error: locator.click: Target page, context or browser has been closed
Call log:
  - waiting for getByRole('link', { name: 'Transfer Funds' })

```

# Test source

```ts
  1  | import { Page, expect } from '@playwright/test';
  2  | 
  3  | export class TransactionPage {
  4  | 
  5  |     constructor(private page: Page) {}
  6  | 
  7  |     async navigateToTransferFunds() {
  8  | 
> 9  |         await this.page.getByRole('link', { name: 'Transfer Funds'}).click();
     |                                                                      ^ Error: locator.click: Target page, context or browser has been closed
  10 |     }
  11 | 
  12 |     async verifyTransferPageLoaded() {
  13 | 
  14 |         await expect( this.page.getByRole('heading', {name: 'Transfer Funds' })).toBeVisible();
  15 |     }
  16 | 
  17 |     async transferAmount(amount: string) {
  18 | 
  19 |         await this.page.locator('#amount').fill(amount);
  20 | 
  21 |         await this.page.locator('#fromAccountId') .selectOption({ index: 0 });
  22 | 
  23 |         const count = await this.page .locator('#toAccountId option') .count();
  24 | 
  25 |         if (count > 1) {
  26 | 
  27 |             await this.page.locator('#toAccountId').selectOption({ index: 1 });
  28 | 
  29 |         } else {
  30 | 
  31 |             await this.page.locator('#toAccountId').selectOption({ index: 0 });
  32 |         }
  33 | 
  34 |         await this.page.locator( 'input[value="Transfer"]').click();
  35 |     }
  36 | 
  37 |     async verifyTransferMessage() {
  38 | 
  39 |         await expect( this.page.locator('body')).toContainText(
  40 |             'Transfer Complete'
  41 |         );
  42 |     }
  43 | }
```