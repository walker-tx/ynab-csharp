<!-- Start SDK Example Usage [usage] -->
```csharp
using WalkerTX.Ynab.SDK;
using WalkerTX.Ynab.SDK.Models.Components;

var sdk = new Ynab(bearer: "<YOUR_BEARER_TOKEN_HERE>");

var res = await sdk.User.GetAsync();

// handle response
```
<!-- End SDK Example Usage [usage] -->