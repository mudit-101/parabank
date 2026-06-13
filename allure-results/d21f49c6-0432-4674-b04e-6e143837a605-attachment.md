# Instructions

- Following Playwright test failed.
- Explain why, be concise, respect Playwright best practices.
- Provide a snippet of code with the fix, if possible.

# Test info

- Name: API\ValidateAccountDetails.spec.ts >> FR-04 Validate Account Details
- Location: tests\API\ValidateAccountDetails.spec.ts:4:5

# Error details

```
Error: expect(received).toContain(expected) // indexOf

Expected substring: "<customerId>undefined</customerId>"
Received string:    ""
```

# Test source

```ts
  1  | import { test, expect } from '@playwright/test';
  2  | import loginData from '../../utils/loginData.json';
  3  | import { getCustomerId } from '../../utils/customerUtils';
  4  | test('FR-04 Validate Account Details', async ({request}) => {
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
  15 |     const responseBody =await response.text();
> 16 |     expect(responseBody).toContain(`<customerId>${customerId}</customerId>`);
     |                          ^ Error: expect(received).toContain(expected) // indexOf
  17 |     expect(responseBody).toContain('<type>CHECKING</type>');
  18 | });
```