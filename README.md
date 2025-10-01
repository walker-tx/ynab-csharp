# WalkerTX.Ynab.SDK

Developer-friendly & type-safe Csharp SDK specifically catered to leverage *WalkerTX.Ynab.SDK* API.

<div align="left">
    <a href="https://www.speakeasy.com/?utm_source=walker-tx-ynab-sdk&utm_campaign=csharp"><img src="https://www.speakeasy.com/assets/badges/built-by-speakeasy.svg" /></a>
    <a href="https://opensource.org/licenses/MIT">
        <img src="https://img.shields.io/badge/License-MIT-blue.svg" style="width: 100px; height: 28px;" />
    </a>
</div>


<br /><br />
> [!IMPORTANT]
> This SDK is not yet ready for production use. To complete setup please follow the steps outlined in your [workspace](https://app.speakeasy.com/org/walker/ynab). Delete this section before > publishing to a package manager.

<!-- Start Summary [summary] -->
## Summary

YNAB API Endpoints: Our API uses a REST based design, leverages the JSON data format, and relies upon HTTPS for transport. We respond with meaningful HTTP response codes and if an error occurs, we include error details in the response body.  API Documentation is at https://api.ynab.com
<!-- End Summary [summary] -->

<!-- Start Table of Contents [toc] -->
## Table of Contents
<!-- $toc-max-depth=2 -->
* [WalkerTX.Ynab.SDK](#walkertxynabsdk)
  * [SDK Installation](#sdk-installation)
  * [SDK Example Usage](#sdk-example-usage)
  * [Authentication](#authentication)
  * [Available Resources and Operations](#available-resources-and-operations)
  * [Error Handling](#error-handling)
  * [Server Selection](#server-selection)
* [Development](#development)
  * [Maturity](#maturity)
  * [Contributions](#contributions)

<!-- End Table of Contents [toc] -->

<!-- Start SDK Installation [installation] -->
## SDK Installation

To add a reference to a local instance of the SDK in a .NET project:
```bash
dotnet add reference src/WalkerTX/Ynab/SDK/WalkerTX.Ynab.SDK.csproj
```
<!-- End SDK Installation [installation] -->

<!-- Start SDK Example Usage [usage] -->
## SDK Example Usage

### Example

```csharp
using WalkerTX.Ynab.SDK;
using WalkerTX.Ynab.SDK.Models.Components;

var sdk = new Ynab(bearer: "<YOUR_BEARER_TOKEN_HERE>");

var res = await sdk.User.GetAsync();

// handle response
```
<!-- End SDK Example Usage [usage] -->

<!-- Start Authentication [security] -->
## Authentication

### Per-Client Security Schemes

This SDK supports the following security scheme globally:

| Name     | Type | Scheme      |
| -------- | ---- | ----------- |
| `Bearer` | http | HTTP Bearer |

To authenticate with the API the `Bearer` parameter must be set when initializing the SDK client instance. For example:
```csharp
using WalkerTX.Ynab.SDK;
using WalkerTX.Ynab.SDK.Models.Components;

var sdk = new Ynab(bearer: "<YOUR_BEARER_TOKEN_HERE>");

var res = await sdk.User.GetAsync();

// handle response
```
<!-- End Authentication [security] -->

<!-- Start Available Resources and Operations [operations] -->
## Available Resources and Operations

<details open>
<summary>Available methods</summary>

### [Accounts](docs/sdks/accounts/README.md)

* [List](docs/sdks/accounts/README.md#list) - Account list
* [Create](docs/sdks/accounts/README.md#create) - Create a new account
* [Get](docs/sdks/accounts/README.md#get) - Single account

### [Budgets](docs/sdks/budgets/README.md)

* [List](docs/sdks/budgets/README.md#list) - List budgets
* [Get](docs/sdks/budgets/README.md#get) - Single budget
* [GetSettings](docs/sdks/budgets/README.md#getsettings) - Budget Settings

### [Categories](docs/sdks/categories/README.md)

* [List](docs/sdks/categories/README.md#list) - List categories
* [Get](docs/sdks/categories/README.md#get) - Single category
* [Update](docs/sdks/categories/README.md#update) - Update a category
* [GetByMonth](docs/sdks/categories/README.md#getbymonth) - Single category for a specific budget month
* [UpdateMonth](docs/sdks/categories/README.md#updatemonth) - Update a category for a specific month

### [Months](docs/sdks/months/README.md)

* [List](docs/sdks/months/README.md#list) - List budget months
* [Get](docs/sdks/months/README.md#get) - Single budget month

### [PayeeLocations](docs/sdks/payeelocations/README.md)

* [List](docs/sdks/payeelocations/README.md#list) - List payee locations
* [Get](docs/sdks/payeelocations/README.md#get) - Single payee location
* [ListByPayee](docs/sdks/payeelocations/README.md#listbypayee) - List locations for a payee

### [Payees](docs/sdks/payees/README.md)

* [List](docs/sdks/payees/README.md#list) - List payees
* [Get](docs/sdks/payees/README.md#get) - Single payee
* [Update](docs/sdks/payees/README.md#update) - Update a payee

### [ScheduledTransactions](docs/sdks/scheduledtransactions/README.md)

* [List](docs/sdks/scheduledtransactions/README.md#list) - List scheduled transactions
* [Create](docs/sdks/scheduledtransactions/README.md#create) - Create a single scheduled transaction
* [Get](docs/sdks/scheduledtransactions/README.md#get) - Single scheduled transaction
* [Update](docs/sdks/scheduledtransactions/README.md#update) - Updates an existing scheduled transaction
* [Delete](docs/sdks/scheduledtransactions/README.md#delete) - Deletes an existing scheduled transaction

### [Transactions](docs/sdks/transactions/README.md)

* [List](docs/sdks/transactions/README.md#list) - List transactions
* [Create](docs/sdks/transactions/README.md#create) - Create a single transaction or multiple transactions
* [UpdateMany](docs/sdks/transactions/README.md#updatemany) - Update multiple transactions
* [Import](docs/sdks/transactions/README.md#import) - Import transactions
* [Get](docs/sdks/transactions/README.md#get) - Single transaction
* [UpdateOne](docs/sdks/transactions/README.md#updateone) - Updates an existing transaction
* [Delete](docs/sdks/transactions/README.md#delete) - Deletes an existing transaction
* [ListByAccount](docs/sdks/transactions/README.md#listbyaccount) - List account transactions
* [ListByCategory](docs/sdks/transactions/README.md#listbycategory) - List category transactions, excluding any pending transactions
* [ListByPayee](docs/sdks/transactions/README.md#listbypayee) - List payee transactions, excluding any pending transactions
* [ListByMonth](docs/sdks/transactions/README.md#listbymonth) - List transactions in month, excluding any pending transactions

### [User](docs/sdks/user/README.md)

* [Get](docs/sdks/user/README.md#get) - User info


</details>
<!-- End Available Resources and Operations [operations] -->

<!-- Start Error Handling [errors] -->
## Error Handling

[`YnabException`](./src/WalkerTX/Ynab/SDK/Models/Errors/YnabException.cs) is the base exception class for all HTTP error responses. It has the following properties:

| Property      | Type                  | Description           |
|---------------|-----------------------|-----------------------|
| `Message`     | *string*              | Error message         |
| `Request`     | *HttpRequestMessage*  | HTTP request object   |
| `Response`    | *HttpResponseMessage* | HTTP response object  |

Some exceptions in this SDK include an additional `Payload` field, which will contain deserialized custom error data when present. Possible exceptions are listed in the [Error Classes](#error-classes) section.

### Example

```csharp
using WalkerTX.Ynab.SDK;
using WalkerTX.Ynab.SDK.Models.Components;
using WalkerTX.Ynab.SDK.Models.Errors;

var sdk = new Ynab(bearer: "<YOUR_BEARER_TOKEN_HERE>");

try
{
    var res = await sdk.User.GetAsync();

    // handle response
}
catch (YnabException ex)  // all SDK exceptions inherit from YnabException
{
    // ex.ToString() provides a detailed error message
    System.Console.WriteLine(ex);

    // Base exception fields
    HttpRequestMessage request = ex.Request;
    HttpResponseMessage response = ex.Response;
    var statusCode = (int)response.StatusCode;
    var responseBody = ex.Body;

    if (ex is ErrorResponse) // different exceptions may be thrown depending on the method
    {
        // Check error data fields
        ErrorResponsePayload payload = ex.Payload;
        ErrorDetail Error = payload.Error;
        HTTPMetadata HttpMeta = payload.HttpMeta;
    }

    // An underlying cause may be provided
    if (ex.InnerException != null)
    {
        Exception cause = ex.InnerException;
    }
}
catch (System.Net.Http.HttpRequestException ex)
{
    // Check ex.InnerException for Network connectivity errors
}
```

### Error Classes

**Primary exceptions:**
* [`YnabException`](./src/WalkerTX/Ynab/SDK/Models/Errors/YnabException.cs): The base class for HTTP error responses.
  * [`ErrorResponse`](./src/WalkerTX/Ynab/SDK/Models/Errors/ErrorResponse.cs): Generic error.

<details><summary>Less common exceptions (2)</summary>

* [`System.Net.Http.HttpRequestException`](https://learn.microsoft.com/en-us/dotnet/api/system.net.http.httprequestexception): Network connectivity error. For more details about the underlying cause, inspect the `ex.InnerException`.

* Inheriting from [`YnabException`](./src/WalkerTX/Ynab/SDK/Models/Errors/YnabException.cs):
  * [`ResponseValidationError`](./src/WalkerTX/Ynab/SDK/Models/Errors/ResponseValidationError.cs): Thrown when the response data could not be deserialized into the expected type.
</details>
<!-- End Error Handling [errors] -->

<!-- Start Server Selection [server] -->
## Server Selection

### Override Server URL Per-Client

The default server can be overridden globally by passing a URL to the `serverUrl: string` optional parameter when initializing the SDK client instance. For example:
```csharp
using WalkerTX.Ynab.SDK;
using WalkerTX.Ynab.SDK.Models.Components;

var sdk = new Ynab(
    serverUrl: "https://api.ynab.com/v1",
    bearer: "<YOUR_BEARER_TOKEN_HERE>"
);

var res = await sdk.User.GetAsync();

// handle response
```
<!-- End Server Selection [server] -->

<!-- Placeholder for Future Speakeasy SDK Sections -->

# Development

## Maturity

This SDK is in beta, and there may be breaking changes between versions without a major version update. Therefore, we recommend pinning usage
to a specific package version. This way, you can install the same version each time without breaking changes unless you are intentionally
looking for the latest version.

## Contributions

While we value open-source contributions to this SDK, this library is generated programmatically. Any manual changes added to internal files will be overwritten on the next generation. 
We look forward to hearing your feedback. Feel free to open a PR or an issue with a proof of concept and we'll do our best to include it in a future release. 

### SDK Created by [Speakeasy](https://www.speakeasy.com/?utm_source=walker-tx-ynab-sdk&utm_campaign=csharp)
