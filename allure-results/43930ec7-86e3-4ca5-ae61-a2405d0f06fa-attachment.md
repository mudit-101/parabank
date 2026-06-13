# Instructions

- Following Playwright test failed.
- Explain why, be concise, respect Playwright best practices.
- Provide a snippet of code with the fix, if possible.

# Test info

- Name: API\GetAccounts.spec.ts >> FR-02 Get Accounts List
- Location: tests\API\GetAccounts.spec.ts:4:5

# Error details

```
Error: expect(received).toBe(expected) // Object.is equality

Expected: 200
Received: 404
```

# Test source

```ts
  1  | import { test, expect } from '@playwright/test';
  2  | import loginData from '../../utils/loginData.json';
  3  | import { getCustomerId } from '../../utils/customerUtils';
  4  | test('FR-02 Get Accounts List', async ({request}) => {
  5  |     const customerId =
  6  |         await getCustomerId(
  7  |             request,
  8  |             loginData.validUser.username,
  9  |             loginData.validUser.password
  10 |         );
  11 | 
  12 |     const response = await request.get(
  13 |         `https://parabank.parasoft.com/parabank/services/bank/customers/${customerId}/accounts`
  14 |     );
> 15 |     expect(response.status()).toBe(200);
     |                               ^ Error: expect(received).toBe(expected) // Object.is equality
  16 |     const responseBody =await response.text();
  17 |     expect(responseBody).toContain('<accounts>');
  18 | });
```