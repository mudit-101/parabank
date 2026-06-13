# Instructions

- Following Playwright test failed.
- Explain why, be concise, respect Playwright best practices.
- Provide a snippet of code with the fix, if possible.

# Test info

- Name: API\ValidateAccountExists.spec.ts >> FR-03 Validate Account Exists
- Location: tests\API\ValidateAccountExists.spec.ts:4:5

# Error details

```
Error: expect(received).toContain(expected) // indexOf

Expected substring: "<id>"
Received string:    ""
```

# Test source

```ts
  1  | import { test, expect } from '@playwright/test';
  2  | import loginData from '../../utils/loginData.json';
  3  | import { getCustomerId } from '../../utils/customerUtils';
  4  | test('FR-03 Validate Account Exists', async ({request}) => {
  5  |     const customerId =
  6  |         await getCustomerId(
  7  |             request,
  8  |             loginData.validUser.username,
  9  |             loginData.validUser.password
  10 |         );
  11 |     const response = await request.get(
  12 |         `https://parabank.parasoft.com/parabank/services/bank/customers/${customerId}/accounts`
  13 |     );
  14 |     const responseBody =await response.text();
> 15 |     expect(responseBody).toContain('<id>');
     |                          ^ Error: expect(received).toContain(expected) // indexOf
  16 | });
```