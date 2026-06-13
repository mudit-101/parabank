# Instructions

- Following Playwright test failed.
- Explain why, be concise, respect Playwright best practices.
- Provide a snippet of code with the fix, if possible.

# Test info

- Name: ui\AccountOverview.spec.ts >> FR-06 Account Overview Validation
- Location: tests\ui\AccountOverview.spec.ts:5:5

# Error details

```
Error: expect(page).toHaveURL(expected) failed

Expected pattern: /overview.htm/
Received string:  "https://parabank.parasoft.com/parabank/login.htm;jsessionid=4BA08ED66030776CDAE0DEDBB4CC5A6E"
Timeout: 5000ms

Call log:
  - Expect "toHaveURL" with timeout 5000ms
    13 × unexpected value "https://parabank.parasoft.com/parabank/login.htm;jsessionid=4BA08ED66030776CDAE0DEDBB4CC5A6E"

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
  3  | import { AccountOverviewPage } from '../../pages/AccountOverviewPage';
  4  | import loginData from '../../utils/loginData.json';
  5  | test('FR-06 Account Overview Validation', async ({page}) => {
  6  |     const loginPage = new LoginPage(page);
  7  |     const accountOverviewPage =new AccountOverviewPage(page);
  8  |     // Navigate to Login Page
  9  |     await loginPage.navigateToLoginPage();
  10 |     // Login
  11 |     await loginPage.login(
  12 |         loginData.validUser.username,
  13 |         loginData.validUser.password
  14 |     );
  15 |     // Verify Login Successful
> 16 |     await expect(page).toHaveURL(/overview.htm/);
     |                        ^ Error: expect(page).toHaveURL(expected) failed
  17 |     // Navigate to Accounts Overview
  18 |     await accountOverviewPage.navigateToAccountsOverview();
  19 |     // Verify Accounts Overview Page
  20 |     await accountOverviewPage.verifyAccountsOverviewDisplayed();
  21 |     // Take Screenshot
  22 |     await accountOverviewPage.captureOverviewScreenshot();
  23 |     console.log('Accounts Overview Page Verified Successfully');
  24 | });
```