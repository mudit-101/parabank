# Instructions

- Following Playwright test failed.
- Explain why, be concise, respect Playwright best practices.
- Provide a snippet of code with the fix, if possible.

# Test info

- Name: ui\TransferFunds.spec.ts >> FR-05 Transfer Funds
- Location: tests\ui\TransferFunds.spec.ts:6:5

# Error details

```
Error: expect(page).toHaveURL(expected) failed

Expected pattern: /overview.htm/
Received string:  "https://parabank.parasoft.com/parabank/login.htm;jsessionid=45B9981F626374683733B2F91A7B8349"

Call log:
  - Expect "toHaveURL" with timeout 5000ms
    10 × unexpected value "https://parabank.parasoft.com/parabank/login.htm;jsessionid=45B9981F626374683733B2F91A7B8349"

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
  1  | import { test, expect } from '@playwright/test';
  2  | import { LoginPage } from '../../pages/LoginPage';
  3  | import { TransferFundsPage } from '../../pages/TransferFundsPage';
  4  | import loginData from '../../utils/loginData.json';
  5  | 
  6  | test(
  7  |     'FR-05 Transfer Funds',
  8  |     async ({ page }) => {
  9  | 
  10 |         const loginPage =
  11 |             new LoginPage(page);
  12 | 
  13 |         const transferFundsPage =
  14 |             new TransferFundsPage(page);
  15 | 
  16 |         await loginPage.navigateToLoginPage();
  17 | 
  18 |         await loginPage.login(
  19 |             loginData.validUser.username,
  20 |             loginData.validUser.password
  21 |         );
  22 | 
  23 |         await expect(page)
> 24 |             .toHaveURL(/overview.htm/);
     |              ^ Error: expect(page).toHaveURL(expected) failed
  25 | 
  26 |         await transferFundsPage
  27 |             .navigateToTransferFundsPage();
  28 | 
  29 |         const accounts =
  30 |             await transferFundsPage.getSelectedAccounts();
  31 | 
  32 |         await transferFundsPage.transferFunds(
  33 |             '100',
  34 |             accounts.fromAccount,
  35 |             accounts.toAccount
  36 |         );
  37 | 
  38 |         await transferFundsPage
  39 |             .verifyTransferCompleted();
  40 |     }
  41 | );
```