# Instructions

- Following Playwright test failed.
- Explain why, be concise, respect Playwright best practices.
- Provide a snippet of code with the fix, if possible.

# Test info

- Name: ui\TransferFunds.spec.ts >> FR-05 Transfer Funds
- Location: tests\ui\TransferFunds.spec.ts:5:5

# Error details

```
Error: expect(page).toHaveURL(expected) failed

Expected pattern: /overview.htm/
Received string:  ""

Call log:
  - Expect "toHaveURL" with timeout 5000ms

```

# Test source

```ts
  1  | import { test, expect } from '@playwright/test';
  2  | import { LoginPage } from '../../pages/LoginPage';
  3  | import { TransferFundsPage } from '../../pages/TransferFundsPage';
  4  | import loginData from '../../utils/loginData.json';
  5  | test('FR-05 Transfer Funds', async ({page}) => {
  6  |     const loginPage = new LoginPage(page);
  7  |     const transferFundsPage = new TransferFundsPage(page);
  8  |     await loginPage.navigateToLoginPage();
  9  |     await loginPage.login(
  10 |         loginData.validUser.username,
  11 |         loginData.validUser.password
  12 |     );
> 13 |     await expect(page).toHaveURL(/overview.htm/);
     |                        ^ Error: expect(page).toHaveURL(expected) failed
  14 |     await transferFundsPage.navigateToTransferFundsPage();
  15 |     await transferFundsPage .transferFunds('100');
  16 |     await transferFundsPage.verifyTransferCompleted();
  17 | });
```