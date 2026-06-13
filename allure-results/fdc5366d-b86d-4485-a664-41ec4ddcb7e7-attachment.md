# Instructions

- Following Playwright test failed.
- Explain why, be concise, respect Playwright best practices.
- Provide a snippet of code with the fix, if possible.

# Test info

- Name: API\AccountAPI.spec.ts >> Scenario 2 - Get Accounts API
- Location: tests\API\AccountAPI.spec.ts:4:5

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
  4  | test('Scenario 2 - Get Accounts API', async ({request}) => {
  5  |     const customerId =
  6  |         await getCustomerId(
  7  |             request,
  8  |             loginData.validUser.username,
  9  |             loginData.validUser.password
  10 |         );
  11 | 
  12 |     console.log('Customer ID:', customerId);
  13 | 
  14 |     const response = await request.get(
  15 |         `https://parabank.parasoft.com/parabank/services/bank/customers/${customerId}/accounts`
  16 |     );
> 17 |     expect(response.status()).toBe(200);
     |                               ^ Error: expect(received).toBe(expected) // Object.is equality
  18 |     const responseBody = await response.text();
  19 |     console.log(responseBody);
  20 |     expect(responseBody).not.toBeNull();
  21 |     console.log(await response.text());
  22 | 
  23 | });
```