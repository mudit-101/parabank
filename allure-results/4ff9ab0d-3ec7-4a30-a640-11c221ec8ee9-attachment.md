# Instructions

- Following Playwright test failed.
- Explain why, be concise, respect Playwright best practices.
- Provide a snippet of code with the fix, if possible.

# Test info

- Name: e2e\TransferAndValidate.spec.ts >> scen-7 and scen-8 validate transfer money
- Location: tests\e2e\TransferAndValidate.spec.ts:7:5

# Error details

```
Test timeout of 30000ms exceeded.
```

```
Error: page.waitForFunction: Test timeout of 30000ms exceeded.
```

# Page snapshot

```yaml
- generic [active] [ref=e1]:
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
        - paragraph [ref=e29]: Welcome John Smith
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
        - heading "Transfer Funds" [level=1] [ref=e51]
        - generic [ref=e52]:
          - paragraph [ref=e53]:
            - text: "Amount: $"
            - textbox [ref=e54]
          - generic [ref=e55]:
            - text: "From account #"
            - combobox [ref=e56]:
              - option "13344" [selected]
            - text: "to account #"
            - combobox [ref=e57]:
              - option "13344" [selected]
          - button "Transfer" [ref=e59] [cursor=pointer]
  - generic [ref=e61]:
    - list [ref=e62]:
      - listitem [ref=e63]:
        - link "Home" [ref=e64] [cursor=pointer]:
          - /url: index.htm
        - text: "|"
      - listitem [ref=e65]:
        - link "About Us" [ref=e66] [cursor=pointer]:
          - /url: about.htm
        - text: "|"
      - listitem [ref=e67]:
        - link "Services" [ref=e68] [cursor=pointer]:
          - /url: services.htm
        - text: "|"
      - listitem [ref=e69]:
        - link "Products" [ref=e70] [cursor=pointer]:
          - /url: http://www.parasoft.com/jsp/products.jsp
        - text: "|"
      - listitem [ref=e71]:
        - link "Locations" [ref=e72] [cursor=pointer]:
          - /url: http://www.parasoft.com/jsp/pr/contacts.jsp
        - text: "|"
      - listitem [ref=e73]:
        - link "Forum" [ref=e74] [cursor=pointer]:
          - /url: http://forums.parasoft.com/
        - text: "|"
      - listitem [ref=e75]:
        - link "Site Map" [ref=e76] [cursor=pointer]:
          - /url: sitemap.htm
        - text: "|"
      - listitem [ref=e77]:
        - link "Contact Us" [ref=e78] [cursor=pointer]:
          - /url: contact.htm
    - paragraph [ref=e79]: © Parasoft. All rights reserved.
    - list [ref=e80]:
      - listitem [ref=e81]: "Visit us at:"
      - listitem [ref=e82]:
        - link "www.parasoft.com" [ref=e83] [cursor=pointer]:
          - /url: http://www.parasoft.com/
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
     |                         ^ Error: page.waitForFunction: Test timeout of 30000ms exceeded.
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