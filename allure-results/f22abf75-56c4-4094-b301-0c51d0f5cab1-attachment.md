# Instructions

- Following Playwright test failed.
- Explain why, be concise, respect Playwright best practices.
- Provide a snippet of code with the fix, if possible.

# Test info

- Name: ui\AccountOverview.spec.ts >> scen-6 Account Overview Validation
- Location: tests\ui\AccountOverview.spec.ts:5:5

# Error details

```
Error: browserContext.close: Test ended.
Browser logs:

<launching> C:\Users\HP\AppData\Local\ms-playwright\firefox-1522\firefox\firefox.exe -no-remote -wait-for-browser -foreground -profile C:\Users\HP\AppData\Local\Temp\playwright_firefoxdev_profile-Z3jWL3 -juggler-pipe -silent
<launched> pid=4772
[pid=4772][err] JavaScript warning: resource://services-settings/Utils.sys.mjs, line 119: unreachable code after return statement
[pid=4772][out] 
[pid=4772][out] Juggler listening to the pipe
[pid=4772][out] console.error: "Warning: unrecognized command line flag" "-foreground"
```