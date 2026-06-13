# Instructions

- Following Playwright test failed.
- Explain why, be concise, respect Playwright best practices.
- Provide a snippet of code with the fix, if possible.

# Test info

- Name: e2e\TransferAndValidate.spec.ts >> FR-06 & FR-07 Transfer Funds and Validate Balance
- Location: tests\e2e\TransferAndValidate.spec.ts:7:5

# Error details

```
Error: expect(page).toHaveURL(expected) failed

Expected pattern: /overview.htm/
Received string:  "https://parabank.parasoft.com/parabank/login.htm;jsessionid=50346B238DBBEAA498AEBDC655F9C7BE"

Call log:
  - Expect "toHaveURL" with timeout 5000ms
    9 × unexpected value "https://parabank.parasoft.com/parabank/login.htm;jsessionid=50346B238DBBEAA498AEBDC655F9C7BE"

```

```yaml
- link:
  - /url: admin.htm
  - img
- link "ParaBank":
  - /url: index.htm
  - img "ParaBank"
- paragraph: Experience the difference
- list:
  - listitem: Solutions
  - listitem:
    - link "About Us":
      - /url: about.htm
  - listitem:
    - link "Services":
      - /url: services.htm
  - listitem:
    - link "Products":
      - /url: http://www.parasoft.com/jsp/products.jsp
  - listitem:
    - link "Locations":
      - /url: http://www.parasoft.com/jsp/pr/contacts.jsp
  - listitem:
    - link "Admin Page":
      - /url: admin.htm
- list:
  - listitem:
    - link "home":
      - /url: index.htm
  - listitem:
    - link "about":
      - /url: about.htm
  - listitem:
    - link "contact":
      - /url: contact.htm
- heading "Customer Login" [level=2]
- paragraph: Username
- textbox
- paragraph: Password
- textbox
- button "Log In"
- paragraph:
  - link "Forgot login info?":
    - /url: lookup.htm
- paragraph:
  - link "Register":
    - /url: register.htm
- heading "Error!" [level=1]
- paragraph: The username and password could not be verified.
- list:
  - listitem:
    - link "Home":
      - /url: index.htm
    - text: "|"
  - listitem:
    - link "About Us":
      - /url: about.htm
    - text: "|"
  - listitem:
    - link "Services":
      - /url: services.htm
    - text: "|"
  - listitem:
    - link "Products":
      - /url: http://www.parasoft.com/jsp/products.jsp
    - text: "|"
  - listitem:
    - link "Locations":
      - /url: http://www.parasoft.com/jsp/pr/contacts.jsp
    - text: "|"
  - listitem:
    - link "Forum":
      - /url: http://forums.parasoft.com/
    - text: "|"
  - listitem:
    - link "Site Map":
      - /url: sitemap.htm
    - text: "|"
  - listitem:
    - link "Contact Us":
      - /url: contact.htm
- paragraph: © Parasoft. All rights reserved.
- list:
  - listitem: "Visit us at:"
  - listitem:
    - link "www.parasoft.com":
      - /url: http://www.parasoft.com/
```

# Test source

```ts
  1   | import { test, expect } from '@playwright/test';
  2   | import { LoginPage } from '../../pages/LoginPage';
  3   | import { TransferFundsPage } from '../../pages/TransferFundsPage';
  4   | import { getAccountDetails } from '../../fixtures/accountFixture';
  5   | import loginData from '../../utils/loginData.json';
  6   | 
  7   | test('FR-06 & FR-07 Transfer Funds and Validate Balance', async ({ page, request }) => {
  8   | 
  9   |     const loginPage = new LoginPage(page);
  10  |     const transferFundsPage = new TransferFundsPage(page);
  11  | 
  12  |     await loginPage.navigateToLoginPage();
  13  | 
  14  |     await loginPage.login(
  15  |         loginData.validUser.username,
  16  |         loginData.validUser.password
  17  |     );
  18  | 
> 19  |     await expect(page).toHaveURL(/overview.htm/);
      |                        ^ Error: expect(page).toHaveURL(expected) failed
  20  | 
  21  |     await transferFundsPage.navigateToTransferFundsPage();
  22  | 
  23  |     const accounts =
  24  |         await transferFundsPage.getSelectedAccounts();
  25  | 
  26  |     const fromAccount =
  27  |         accounts.fromAccount;
  28  | 
  29  |     const toAccount =
  30  |         accounts.toAccount;
  31  | 
  32  |     console.log(
  33  |         'Validating Account:',
  34  |         fromAccount
  35  |     );
  36  | 
  37  |     console.log(
  38  |         'Fetching balance before transfer'
  39  |     );
  40  | 
  41  |     const beforeTransfer =
  42  |         await getAccountDetails(
  43  |             request,
  44  |             fromAccount
  45  |         );
  46  | 
  47  |     console.log(
  48  |         'Before Transfer:',
  49  |         beforeTransfer
  50  |     );
  51  | 
  52  |     await transferFundsPage.transferFunds(
  53  |         '100',
  54  |         fromAccount,
  55  |         toAccount
  56  |     );
  57  | 
  58  |     await transferFundsPage.verifyTransferCompleted();
  59  | 
  60  |     await page.waitForTimeout(3000);
  61  | 
  62  |     console.log(
  63  |         'Fetching balance after transfer'
  64  |     );
  65  | 
  66  |     const afterTransfer =
  67  |         await getAccountDetails(
  68  |             request,
  69  |             fromAccount
  70  |         );
  71  | 
  72  |     console.log(
  73  |         'After Transfer:',
  74  |         afterTransfer
  75  |     );
  76  | 
  77  |     expect(afterTransfer)
  78  |         .toContain('<account>');
  79  | 
  80  |     expect(afterTransfer)
  81  |         .toContain('<balance>');
  82  | 
  83  |     expect(afterTransfer)
  84  |         .not.toContain(
  85  |             'Could not find account'
  86  |         );
  87  | 
  88  |     if (beforeTransfer !== afterTransfer) {
  89  | 
  90  |         console.log(
  91  |             'Balance updated successfully'
  92  |         );
  93  | 
  94  |     } else {
  95  | 
  96  |         console.log(
  97  |             'Balance did not change'
  98  |         );
  99  |     }
  100 | 
  101 |     await page.screenshot({
  102 |         path: 'screenshots/FR06_FR07.png'
  103 |     });
  104 | });
```