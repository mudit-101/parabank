# Instructions

- Following Playwright test failed.
- Explain why, be concise, respect Playwright best practices.
- Provide a snippet of code with the fix, if possible.

# Test info

- Name: API\ApiResponesTime.spec.ts >> TS14 API Response Time
- Location: tests\API\ApiResponesTime.spec.ts:4:5

# Error details

```
Error: expect(received).toBe(expected) // Object.is equality

Expected: 200
Received: 404
```

# Test source

```ts
  1  | import {test,expect} from "@playwright/test";
  2  | import loginData from '../../utils/loginData.json';
  3  | import { getCustomerId } from '../../utils/customerUtils';
  4  | test('TS14 API Response Time', async ({request}) =>{
  5  |      const customerId =
  6  |         await getCustomerId(
  7  |             request,
  8  |             loginData.validUser.username,
  9  |             loginData.validUser.password
  10 |         );
  11 | 
  12 |     console.log('Customer ID:', customerId);
  13 |     let startTime =Date.now();
  14 |     let r1 = await request.get(`https://parabank.parasoft.com/parabank/services/bank/customers/${customerId}/accounts`);
  15 |     let endTime = Date.now();
  16 |     let responseTime = endTime - startTime;
  17 |     console.log("Response Time :",responseTime );
> 18 |     expect(r1.status()).toBe(200);
     |                         ^ Error: expect(received).toBe(expected) // Object.is equality
  19 |     expect(responseTime).toBeLessThan(2000);
  20 | });
```