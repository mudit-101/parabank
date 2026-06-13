# Instructions

- Following Playwright test failed.
- Explain why, be concise, respect Playwright best practices.
- Provide a snippet of code with the fix, if possible.

# Test info

- Name: e2e\TransferAndValidate.spec.ts >> FR-06 & FR-07 Transfer Funds and Validate Balance
- Location: tests\e2e\TransferAndValidate.spec.ts:7:5

# Error details

```
Error: At least 2 accounts are required for transfer
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
        - paragraph [ref=e29]: Welcome Mudit Goyal
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
            - textbox [active] [ref=e54]: "100"
          - generic [ref=e55]:
            - text: "From account #"
            - combobox [ref=e56]
            - text: "to account #"
            - combobox [ref=e57]
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
  17 |     await this.page.locator('#fromAccountId')
  18 |         .waitFor({ state: 'visible' });
  19 | 
  20 |     await this.page.locator('#toAccountId')
  21 |         .waitFor({ state: 'visible' });
  22 | 
  23 |     const fromOptions =
  24 |         await this.page.locator('#fromAccountId option')
  25 |             .count();
  26 | 
  27 |     const toOptions =
  28 |         await this.page.locator('#toAccountId option')
  29 |             .count();
  30 | 
  31 |     if (fromOptions < 2 || toOptions < 2) {
> 32 |         throw new Error(
     |               ^ Error: At least 2 accounts are required for transfer
  33 |             'At least 2 accounts are required for transfer'
  34 |         );
  35 |     }
  36 | 
  37 |     await this.page.locator('#fromAccountId')
  38 |         .selectOption({ index: 1 });
  39 | 
  40 |     await this.page.locator('#toAccountId')
  41 |         .selectOption({ index: 2 });
  42 | 
  43 |     const fromAccount =
  44 |         await this.page.locator('#fromAccountId')
  45 |             .inputValue();
  46 | 
  47 |     const toAccount =
  48 |         await this.page.locator('#toAccountId')
  49 |             .inputValue();
  50 | 
  51 |     console.log(`From Account: ${fromAccount}`);
  52 |     console.log(`To Account: ${toAccount}`);
  53 | 
  54 |     await this.page.locator(
  55 |         'input[value="Transfer"]'
  56 |     ).click();
  57 | 
  58 |     console.log(`Transferred Amount: ${amount}`);
  59 | 
  60 |     return {
  61 |         fromAccount,
  62 |         toAccount
  63 |     };
  64 | }
  65 | 
  66 |    async verifyTransferCompleted() {
  67 | 
  68 |     await this.page.waitForLoadState('networkidle');
  69 | 
  70 |     await expect(
  71 |     this.page.locator('#showResult')
  72 |    ).toContainText('Transfer Complete');
  73 | 
  74 |     console.log(
  75 |     'Transfer completed successfully'
  76 |      );
  77 | 
  78 |     await this.page.screenshot({
  79 |         path: 'screenshots/transfer-completed.png',
  80 |         fullPage: true
  81 |     });
  82 | }
  83 | }
```