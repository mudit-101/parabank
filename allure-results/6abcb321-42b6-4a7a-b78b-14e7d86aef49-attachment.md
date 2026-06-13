# Instructions

- Following Playwright test failed.
- Explain why, be concise, respect Playwright best practices.
- Provide a snippet of code with the fix, if possible.

# Test info

- Name: e2e\TransferAndValidate.spec.ts >> FR-06 & FR-07 Transfer Funds and Validate Balance
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
            - textbox [ref=e54]
          - generic [ref=e55]:
            - text: "From account #"
            - combobox [ref=e56]:
              - option "22002" [selected]
            - text: "to account #"
            - combobox [ref=e57]:
              - option "22002" [selected]
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
  1   | import { Page, expect } from '@playwright/test';
  2   | 
  3   | export class TransferFundsPage {
  4   | 
  5   |     constructor(private page: Page) {}
  6   | 
  7   |     async navigateToTransferFundsPage() {
  8   | 
  9   |         await this.page.getByRole('link', {
  10  |             name: 'Transfer Funds'
  11  |         }).click();
  12  | 
  13  |         await expect(
  14  |             this.page.getByRole('heading', {
  15  |                 name: 'Transfer Funds'
  16  |             })
  17  |         ).toBeVisible();
  18  |     }
  19  | 
  20  |     async getSelectedAccounts() {
  21  | 
> 22  |         await this.page.waitForFunction(() => {
      |                         ^ Error: page.waitForFunction: Test timeout of 30000ms exceeded.
  23  |             return document.querySelectorAll(
  24  |                 '#fromAccountId option'
  25  |             ).length > 1;
  26  |         });
  27  | 
  28  |         const accounts = await this.page
  29  |             .locator('#fromAccountId option')
  30  |             .evaluateAll(options =>
  31  |                 options.map(
  32  |                     option =>
  33  |                         (option as HTMLOptionElement).value
  34  |                 )
  35  |             );
  36  | 
  37  |         console.log(
  38  |             'Available Accounts:',
  39  |             accounts
  40  |         );
  41  | 
  42  |         return {
  43  |             fromAccount: accounts[0],
  44  |             toAccount: accounts[1]
  45  |         };
  46  |     }
  47  | 
  48  |     async transferFunds(
  49  |         amount: string,
  50  |         fromAccount: string,
  51  |         toAccount: string
  52  |     ) {
  53  | 
  54  |         await this.page.locator('#amount')
  55  |             .fill(amount);
  56  | 
  57  |         await this.page.locator('#fromAccountId')
  58  |             .selectOption(fromAccount);
  59  | 
  60  |         await this.page.locator('#toAccountId')
  61  |             .selectOption(toAccount);
  62  | 
  63  |         console.log(
  64  |             `From Account: ${fromAccount}`
  65  |         );
  66  | 
  67  |         console.log(
  68  |             `To Account: ${toAccount}`
  69  |         );
  70  | 
  71  |         await this.page.locator(
  72  |             'input[value="Transfer"]'
  73  |         ).click();
  74  | 
  75  |         console.log(
  76  |             `Transferred Amount: ${amount}`
  77  |         );
  78  |     }
  79  | 
  80  |     async verifyTransferCompleted() {
  81  | 
  82  |         await this.page.waitForLoadState(
  83  |             'networkidle'
  84  |         );
  85  | 
  86  |         await expect(
  87  |             this.page.locator('#showResult')
  88  |         ).toContainText(
  89  |             'Transfer Complete'
  90  |         );
  91  | 
  92  |         console.log(
  93  |             'Transfer completed successfully'
  94  |         );
  95  | 
  96  |         await this.page.screenshot({
  97  |             path: 'screenshots/transfer-completed.png',
  98  |             fullPage: true
  99  |         });
  100 |     }
  101 | }
```