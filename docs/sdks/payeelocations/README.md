# PayeeLocations
(*PayeeLocations*)

## Overview

### Available Operations

* [List](#list) - List payee locations
* [Get](#get) - Single payee location
* [ListByPayee](#listbypayee) - List locations for a payee

## List

Returns all payee locations

### Example Usage

<!-- UsageSnippet language="csharp" operationID="getPayeeLocations" method="get" path="/budgets/{budget_id}/payee_locations" -->
```csharp
using WalkerTX.Ynab.SDK;
using WalkerTX.Ynab.SDK.Models.Components;

var sdk = new Ynab(bearer: "<YOUR_BEARER_TOKEN_HERE>");

var res = await sdk.PayeeLocations.ListAsync(budgetId: "<id>");

// handle response
```

### Parameters

| Parameter                                                                                                                                                                                         | Type                                                                                                                                                                                              | Required                                                                                                                                                                                          | Description                                                                                                                                                                                       |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `BudgetId`                                                                                                                                                                                        | *string*                                                                                                                                                                                          | :heavy_check_mark:                                                                                                                                                                                | The id of the budget. "last-used" can be used to specify the last used budget and "default" can be used if default budget selection is enabled (see: https://api.ynab.com/#oauth-default-budget). |

### Response

**[GetPayeeLocationsResponse](../../Models/Requests/GetPayeeLocationsResponse.md)**

### Errors

| Error Type                                    | Status Code                                   | Content Type                                  |
| --------------------------------------------- | --------------------------------------------- | --------------------------------------------- |
| WalkerTX.Ynab.SDK.Models.Errors.ErrorResponse | 404                                           | application/json                              |
| WalkerTX.Ynab.SDK.Models.Errors.ErrorResponse | default                                       | application/json                              |
| WalkerTX.Ynab.SDK.Models.Errors.APIException  | 4XX, 5XX                                      | \*/\*                                         |

## Get

Returns a single payee location

### Example Usage

<!-- UsageSnippet language="csharp" operationID="getPayeeLocationById" method="get" path="/budgets/{budget_id}/payee_locations/{payee_location_id}" -->
```csharp
using WalkerTX.Ynab.SDK;
using WalkerTX.Ynab.SDK.Models.Components;

var sdk = new Ynab(bearer: "<YOUR_BEARER_TOKEN_HERE>");

var res = await sdk.PayeeLocations.GetAsync(
    budgetId: "<id>",
    payeeLocationId: "<id>"
);

// handle response
```

### Parameters

| Parameter                                                                                                                                                                                         | Type                                                                                                                                                                                              | Required                                                                                                                                                                                          | Description                                                                                                                                                                                       |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `BudgetId`                                                                                                                                                                                        | *string*                                                                                                                                                                                          | :heavy_check_mark:                                                                                                                                                                                | The id of the budget. "last-used" can be used to specify the last used budget and "default" can be used if default budget selection is enabled (see: https://api.ynab.com/#oauth-default-budget). |
| `PayeeLocationId`                                                                                                                                                                                 | *string*                                                                                                                                                                                          | :heavy_check_mark:                                                                                                                                                                                | id of payee location                                                                                                                                                                              |

### Response

**[GetPayeeLocationByIdResponse](../../Models/Requests/GetPayeeLocationByIdResponse.md)**

### Errors

| Error Type                                    | Status Code                                   | Content Type                                  |
| --------------------------------------------- | --------------------------------------------- | --------------------------------------------- |
| WalkerTX.Ynab.SDK.Models.Errors.ErrorResponse | 404                                           | application/json                              |
| WalkerTX.Ynab.SDK.Models.Errors.ErrorResponse | default                                       | application/json                              |
| WalkerTX.Ynab.SDK.Models.Errors.APIException  | 4XX, 5XX                                      | \*/\*                                         |

## ListByPayee

Returns all payee locations for a specified payee

### Example Usage

<!-- UsageSnippet language="csharp" operationID="getPayeeLocationsByPayee" method="get" path="/budgets/{budget_id}/payees/{payee_id}/payee_locations" -->
```csharp
using WalkerTX.Ynab.SDK;
using WalkerTX.Ynab.SDK.Models.Components;

var sdk = new Ynab(bearer: "<YOUR_BEARER_TOKEN_HERE>");

var res = await sdk.PayeeLocations.ListByPayeeAsync(
    budgetId: "<id>",
    payeeId: "<id>"
);

// handle response
```

### Parameters

| Parameter                                                                                                                                                                                         | Type                                                                                                                                                                                              | Required                                                                                                                                                                                          | Description                                                                                                                                                                                       |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `BudgetId`                                                                                                                                                                                        | *string*                                                                                                                                                                                          | :heavy_check_mark:                                                                                                                                                                                | The id of the budget. "last-used" can be used to specify the last used budget and "default" can be used if default budget selection is enabled (see: https://api.ynab.com/#oauth-default-budget). |
| `PayeeId`                                                                                                                                                                                         | *string*                                                                                                                                                                                          | :heavy_check_mark:                                                                                                                                                                                | id of payee                                                                                                                                                                                       |

### Response

**[GetPayeeLocationsByPayeeResponse](../../Models/Requests/GetPayeeLocationsByPayeeResponse.md)**

### Errors

| Error Type                                    | Status Code                                   | Content Type                                  |
| --------------------------------------------- | --------------------------------------------- | --------------------------------------------- |
| WalkerTX.Ynab.SDK.Models.Errors.ErrorResponse | 404                                           | application/json                              |
| WalkerTX.Ynab.SDK.Models.Errors.ErrorResponse | default                                       | application/json                              |
| WalkerTX.Ynab.SDK.Models.Errors.APIException  | 4XX, 5XX                                      | \*/\*                                         |