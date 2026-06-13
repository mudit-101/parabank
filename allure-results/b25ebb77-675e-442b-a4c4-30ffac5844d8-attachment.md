# Instructions

- Following Playwright test failed.
- Explain why, be concise, respect Playwright best practices.
- Provide a snippet of code with the fix, if possible.

# Test info

- Name: e2e\TransferAndValidate.spec.ts >> FR-06 & FR-07 Transfer Funds and Validate Balance
- Location: tests\e2e\TransferAndValidate.spec.ts:6:5

# Error details

```
Error: expect(page).toHaveURL(expected) failed

Expected pattern: /overview.htm/
Received string:  "https://parabank.parasoft.com/parabank/login.htm;jsessionid=DF0BF9AF47EE1C2C1D6CB9F92889797C"
Timeout: 5000ms

Call log:
  - Expect "toHaveURL" with timeout 5000ms
    14 × unexpected value "https://parabank.parasoft.com/parabank/login.htm;jsessionid=DF0BF9AF47EE1C2C1D6CB9F92889797C"

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
  4  | import { getAccountDetails } from '../../fixtures/accountFixture';
  5  | import loginData from '../../utils/loginData.json';
  6  | test(
  7  |     'FR-06 & FR-07 Transfer Funds and Validate Balance',async ({page,request}) => {
  8  |         const loginPage =new LoginPage(page);
  9  |         const transferFundsPage =new TransferFundsPage(page);
  10 |         // Login
  11 |         await loginPage.navigateToLoginPage();
  12 |         await loginPage.login(
  13 |             loginData.validUser.username,
  14 |             loginData.validUser.password
  15 |         );
> 16 |         await expect(page).toHaveURL(/overview.htm/);
     |                            ^ Error: expect(page).toHaveURL(expected) failed
  17 |         // Source account selected in TransferFundsPage
  18 |         const accountId = '13344';
  19 |         console.log( 'Fetching balance before transfer' );
  20 | 
  21 |         const beforeTransfer = await getAccountDetails(request,accountId);
  22 | 
  23 |         console.log('Before Transfer:', beforeTransfer);
  24 | 
  25 |         // Transfer Funds
  26 |         await transferFundsPage.navigateToTransferFundsPage();
  27 |         await transferFundsPage .transferFunds('100');
  28 |         await transferFundsPage.verifyTransferCompleted();
  29 |         console.log('Fetching balance after transfer');
  30 | 
  31 |         const afterTransfer =await getAccountDetails(request,accountId);
  32 | 
  33 |         console.log('After Transfer:',afterTransfer);
  34 | 
  35 |        // FR-06
  36 |        expect(afterTransfer) .toContain('<account>');
  37 |        expect(afterTransfer).toContain('<balance>');
  38 | // FR-07
  39 |      expect(afterTransfer) .not.toContain('Could not find account');
  40 |     }
  41 | );
```