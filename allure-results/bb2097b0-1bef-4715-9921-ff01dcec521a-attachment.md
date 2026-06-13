# Instructions

- Following Playwright test failed.
- Explain why, be concise, respect Playwright best practices.
- Provide a snippet of code with the fix, if possible.

# Test info

- Name: ui\CreateAccount.spec.ts >> FR-01 Create New Account
- Location: tests\ui\CreateAccount.spec.ts:5:5

# Error details

```
Error: expect(locator).toBeVisible() failed

Locator:  locator('#newAccountId')
Expected: visible
Received: hidden
Timeout:  5000ms

Call log:
  - Expect "toBeVisible" with timeout 5000ms
  - waiting for locator('#newAccountId')
    14 × locator resolved to <a href="" id="newAccountId"></a>
       - unexpected value "hidden"

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
- paragraph: Welcome Mudit Goyal
- heading "Account Services" [level=2]
- list:
  - listitem:
    - link "Open New Account":
      - /url: openaccount.htm
  - listitem:
    - link "Accounts Overview":
      - /url: overview.htm
  - listitem:
    - link "Transfer Funds":
      - /url: transfer.htm
  - listitem:
    - link "Bill Pay":
      - /url: billpay.htm
  - listitem:
    - link "Find Transactions":
      - /url: findtrans.htm
  - listitem:
    - link "Update Contact Info":
      - /url: updateprofile.htm
  - listitem:
    - link "Request Loan":
      - /url: requestloan.htm
  - listitem:
    - link "Log Out":
      - /url: logout.htm
- heading "Open New Account" [level=1]
- paragraph: What type of Account would you like to open?
- combobox:
  - option "CHECKING" [selected]
  - option "SAVINGS"
- paragraph: A minimum of $100.00 must be deposited into this account at time of opening. Please choose an existing account to transfer funds into the new account.
- combobox:
  - option "14898" [selected]
  - option "19449"
- button "Open New Account"
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
  1  | import { Page, expect } from '@playwright/test';
  2  | 
  3  | export class OpenAccountPage {
  4  | 
  5  |     constructor(private page: Page) {}
  6  | 
  7  |     async openNewAccountPage() {
  8  | 
  9  |         await this.page.getByRole('link', {
  10 |             name: 'Open New Account'
  11 |         }).click();
  12 |     }
  13 | 
  14 |     async selectSavingsAccount() {
  15 | 
  16 |         await this.page.selectOption(
  17 |             '#type',
  18 |             '0'
  19 |         );
  20 |     }
  21 | 
  22 |     async clickOpenNewAccount() {
  23 | 
  24 |         await this.page.locator(
  25 |             'input[value="Open New Account"]'
  26 |         ).click();
  27 |     }
  28 | 
  29 |     async verifyAccountCreated() {
  30 | 
  31 |         await this.page.waitForLoadState(
  32 |             'networkidle'
  33 |         );
  34 | 
  35 |         await expect(
  36 |             this.page.locator('#newAccountId')
> 37 |         ).toBeVisible();
     |           ^ Error: expect(locator).toBeVisible() failed
  38 | 
  39 |         const accountId =
  40 |             await this.page
  41 |                 .locator('#newAccountId')
  42 |                 .textContent();
  43 | 
  44 |         console.log(
  45 |             `New Account Created: ${accountId}`
  46 |         );
  47 | 
  48 |         await this.page.screenshot({
  49 |             path: 'screenshots/account-created.png',
  50 |             fullPage: true
  51 |         });
  52 | 
  53 |         return accountId?.trim();
  54 |     }
  55 | }
```