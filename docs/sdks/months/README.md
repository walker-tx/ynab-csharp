# Months
(*Months*)

## Overview

Each budget contains one or more months, which is where Ready to Assign, Age of Money and category (budgeted / activity / balances) amounts are available.

### Available Operations

* [List](#list) - List budget months
* [Get](#get) - Single budget month

## List

Returns all budget months

### Example Usage

<!-- UsageSnippet language="csharp" operationID="getBudgetMonths" method="get" path="/budgets/{budget_id}/months" -->
```csharp
using WalkerTX.Ynab.SDK;
using WalkerTX.Ynab.SDK.Models.Components;

var sdk = new Ynab(bearer: "<YOUR_BEARER_TOKEN_HERE>");

var res = await sdk.Months.ListAsync(budgetId: "<id>");

// handle response
```

### Parameters

| Parameter                                                                                                                                                                                         | Type                                                                                                                                                                                              | Required                                                                                                                                                                                          | Description                                                                                                                                                                                       |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `BudgetId`                                                                                                                                                                                        | *string*                                                                                                                                                                                          | :heavy_check_mark:                                                                                                                                                                                | The id of the budget. "last-used" can be used to specify the last used budget and "default" can be used if default budget selection is enabled (see: https://api.ynab.com/#oauth-default-budget). |
| `LastKnowledgeOfServer`                                                                                                                                                                           | *long*                                                                                                                                                                                            | :heavy_minus_sign:                                                                                                                                                                                | The starting server knowledge.  If provided, only entities that have changed since `last_knowledge_of_server` will be included.                                                                   |

### Response

**[GetBudgetMonthsResponse](../../Models/Requests/GetBudgetMonthsResponse.md)**

### Errors

| Error Type                                    | Status Code                                   | Content Type                                  |
| --------------------------------------------- | --------------------------------------------- | --------------------------------------------- |
| WalkerTX.Ynab.SDK.Models.Errors.ErrorResponse | 404                                           | application/json                              |
| WalkerTX.Ynab.SDK.Models.Errors.ErrorResponse | default                                       | application/json                              |
| WalkerTX.Ynab.SDK.Models.Errors.APIException  | 4XX, 5XX                                      | \*/\*                                         |

## Get

Returns a single budget month

### Example Usage

<!-- UsageSnippet language="csharp" operationID="getBudgetMonth" method="get" path="/budgets/{budget_id}/months/{month}" -->
```csharp
using NodaTime;
using WalkerTX.Ynab.SDK;
using WalkerTX.Ynab.SDK.Models.Components;

var sdk = new Ynab(bearer: "<YOUR_BEARER_TOKEN_HERE>");

var res = await sdk.Months.GetAsync(
    budgetId: "<id>",
    month: LocalDate.FromDateTime(System.DateTime.Parse("2025-03-18"))
);

// handle response
```

### Parameters

| Parameter                                                                                                                                                                                         | Type                                                                                                                                                                                              | Required                                                                                                                                                                                          | Description                                                                                                                                                                                       |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `BudgetId`                                                                                                                                                                                        | *string*                                                                                                                                                                                          | :heavy_check_mark:                                                                                                                                                                                | The id of the budget. "last-used" can be used to specify the last used budget and "default" can be used if default budget selection is enabled (see: https://api.ynab.com/#oauth-default-budget). |
| `Month`                                                                                                                                                                                           | [LocalDate](https://nodatime.org/3.1.x/api/NodaTime.LocalDate.html)                                                                                                                               | :heavy_check_mark:                                                                                                                                                                                | The budget month in ISO format (e.g. 2016-12-01) ("current" can also be used to specify the current calendar month (UTC))                                                                         |

### Response

**[GetBudgetMonthResponse](../../Models/Requests/GetBudgetMonthResponse.md)**

### Errors

| Error Type                                    | Status Code                                   | Content Type                                  |
| --------------------------------------------- | --------------------------------------------- | --------------------------------------------- |
| WalkerTX.Ynab.SDK.Models.Errors.ErrorResponse | 404                                           | application/json                              |
| WalkerTX.Ynab.SDK.Models.Errors.ErrorResponse | default                                       | application/json                              |
| WalkerTX.Ynab.SDK.Models.Errors.APIException  | 4XX, 5XX                                      | \*/\*                                         |