# Instructions

- Following Playwright test failed.
- Explain why, be concise, respect Playwright best practices.
- Provide a snippet of code with the fix, if possible.

# Test info

- Name: e2e\CreateAccAndValidate.spec.ts >> Hybrid Scenario - Create Account and Validate API
- Location: tests\e2e\CreateAccAndValidate.spec.ts:8:5

# Error details

```
Error: expect(locator).toContainText(expected) failed

Locator: locator('.title')
Expected substring: "Account Opened"
Error: strict mode violation: locator('.title') resolved to 3 elements:
    1) <h1 class="title">Open New Account</h1> aka getByRole('heading', { name: 'Open New Account' })
    2) <h1 class="title">Account Opened!</h1> aka getByText('Account Opened!')
    3) <h1 class="title">Error!</h1> aka getByText('Error!')

Call log:
  - Expect "toContainText" with timeout 5000ms
  - waiting for locator('.title')

```

# Page snapshot

```yaml
- generic [ref=e1]:
  - generic [ref=e2]:
    - generic [ref=e3]:
      - link:
        - /url: admin.htm
        - img [ref=e4] [cursor=pointer]
      - link "ParaBank":
        - /url: index.htm
        - img "ParaBank" [ref=e5] [cursor=pointer]
      - paragraph [ref=e6]: Experience the difference
    - generic [ref=e7]:
      - list [ref=e8]:
        - listitem [ref=e9]: Solutions
        - listitem [ref=e10]:
          - link "About Us" [ref=e11] [cursor=pointer]:
            - /url: about.htm
        - listitem [ref=e12]:
          - link "Services" [ref=e13] [cursor=pointer]:
            - /url: services.htm
        - listitem [ref=e14]:
          - link "Products" [ref=e15] [cursor=pointer]:
            - /url: http://www.parasoft.com/jsp/products.jsp
        - listitem [ref=e16]:
          - link "Locations" [ref=e17] [cursor=pointer]:
            - /url: http://www.parasoft.com/jsp/pr/contacts.jsp
        - listitem [ref=e18]:
          - link "Admin Page" [ref=e19] [cursor=pointer]:
            - /url: admin.htm
      - list [ref=e20]:
        - listitem [ref=e21]:
          - link "home" [ref=e22] [cursor=pointer]:
            - /url: index.htm
        - listitem [ref=e23]:
          - link "about" [ref=e24] [cursor=pointer]:
            - /url: about.htm
        - listitem [ref=e25]:
          - link "contact" [ref=e26] [cursor=pointer]:
            - /url: contact.htm
    - generic [ref=e27]:
      - generic [ref=e28]:
        - paragraph [ref=e29]: Welcome JohnAkshaya Yelleti
        - heading "Account Services" [level=2] [ref=e30]
        - list [ref=e31]:
          - listitem [ref=e32]:
            - link "Open New Account" [ref=e33] [cursor=pointer]:
              - /url: openaccount.htm
          - listitem [ref=e34]:
            - link "Accounts Overview" [ref=e35] [cursor=pointer]:
              - /url: overview.htm
          - listitem [ref=e36]:
            - link "Transfer Funds" [ref=e37] [cursor=pointer]:
              - /url: transfer.htm
          - listitem [ref=e38]:
            - link "Bill Pay" [ref=e39] [cursor=pointer]:
              - /url: billpay.htm
          - listitem [ref=e40]:
            - link "Find Transactions" [ref=e41] [cursor=pointer]:
              - /url: findtrans.htm
          - listitem [ref=e42]:
            - link "Update Contact Info" [ref=e43] [cursor=pointer]:
              - /url: updateprofile.htm
          - listitem [ref=e44]:
            - link "Request Loan" [ref=e45] [cursor=pointer]:
              - /url: requestloan.htm
          - listitem [ref=e46]:
            - link "Log Out" [ref=e47] [cursor=pointer]:
              - /url: logout.htm
      - generic [ref=e50]:
        - heading "Open New Account" [level=1] [ref=e51]
        - generic [ref=e52]:
          - paragraph [ref=e53]: What type of Account would you like to open?
          - combobox [ref=e54]:
            - option "CHECKING"
            - option "SAVINGS" [selected]
          - paragraph [ref=e55]: A minimum of $100.00 must be deposited into this account at time of opening. Please choose an existing account to transfer funds into the new account.
          - combobox [ref=e56]:
            - option "12345" [selected]
            - option "12456"
            - option "12567"
            - option "12678"
            - option "12789"
            - option "12900"
            - option "13011"
            - option "13122"
            - option "13233"
            - option "13344"
            - option "14787"
            - option "16785"
            - option "54321"
          - button "Open New Account" [active] [ref=e58] [cursor=pointer]
  - generic [ref=e60]:
    - list [ref=e61]:
      - listitem [ref=e62]:
        - link "Home" [ref=e63] [cursor=pointer]:
          - /url: index.htm
        - text: "|"
      - listitem [ref=e64]:
        - link "About Us" [ref=e65] [cursor=pointer]:
          - /url: about.htm
        - text: "|"
      - listitem [ref=e66]:
        - link "Services" [ref=e67] [cursor=pointer]:
          - /url: services.htm
        - text: "|"
      - listitem [ref=e68]:
        - link "Products" [ref=e69] [cursor=pointer]:
          - /url: http://www.parasoft.com/jsp/products.jsp
        - text: "|"
      - listitem [ref=e70]:
        - link "Locations" [ref=e71] [cursor=pointer]:
          - /url: http://www.parasoft.com/jsp/pr/contacts.jsp
        - text: "|"
      - listitem [ref=e72]:
        - link "Forum" [ref=e73] [cursor=pointer]:
          - /url: http://forums.parasoft.com/
        - text: "|"
      - listitem [ref=e74]:
        - link "Site Map" [ref=e75] [cursor=pointer]:
          - /url: sitemap.htm
        - text: "|"
      - listitem [ref=e76]:
        - link "Contact Us" [ref=e77] [cursor=pointer]:
          - /url: contact.htm
    - paragraph [ref=e78]: © Parasoft. All rights reserved.
    - list [ref=e79]:
      - listitem [ref=e80]: "Visit us at:"
      - listitem [ref=e81]:
        - link "www.parasoft.com" [ref=e82] [cursor=pointer]:
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
  7  |     async navigateToOpenAccountPage() {
  8  | 
  9  |         await this.page.getByRole('link', {
  10 |             name: 'Open New Account'
  11 |         }).click();
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
  46 |     await this.page.waitForLoadState('networkidle');
  47 | 
  48 |     await expect(
  49 |         this.page.locator('.title')
> 50 |     ).toContainText('Account Opened');
     |       ^ Error: expect(locator).toContainText(expected) failed
  51 | 
  52 |     const accountId =
  53 |         await this.page.locator('#newAccountId')
  54 |             .textContent();
  55 | 
  56 |     console.log(
  57 |         `New Account Created: ${accountId}`
  58 |     );
  59 | 
  60 |     await this.page.screenshot({
  61 |         path: 'screenshots/account-created.png',
  62 |         fullPage: true
  63 |     });
  64 | 
  65 |     return accountId?.trim();
  66 | }
  67 | }
```