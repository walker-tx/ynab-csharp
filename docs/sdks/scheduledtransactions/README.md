# ScheduledTransactions
(*ScheduledTransactions*)

## Overview

### Available Operations

* [List](#list) - List scheduled transactions
* [Create](#create) - Create a single scheduled transaction
* [Get](#get) - Single scheduled transaction
* [Update](#update) - Updates an existing scheduled transaction
* [Delete](#delete) - Deletes an existing scheduled transaction

## List

Returns all scheduled transactions

### Example Usage

<!-- UsageSnippet language="csharp" operationID="getScheduledTransactions" method="get" path="/budgets/{budget_id}/scheduled_transactions" -->
```csharp
using WalkerTX.Ynab.SDK;
using WalkerTX.Ynab.SDK.Models.Components;

var sdk = new Ynab(bearer: "<YOUR_BEARER_TOKEN_HERE>");

var res = await sdk.ScheduledTransactions.ListAsync(budgetId: "<id>");

// handle response
```

### Parameters

| Parameter                                                                                                                                                                                         | Type                                                                                                                                                                                              | Required                                                                                                                                                                                          | Description                                                                                                                                                                                       |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `BudgetId`                                                                                                                                                                                        | *string*                                                                                                                                                                                          | :heavy_check_mark:                                                                                                                                                                                | The id of the budget. "last-used" can be used to specify the last used budget and "default" can be used if default budget selection is enabled (see: https://api.ynab.com/#oauth-default-budget). |
| `LastKnowledgeOfServer`                                                                                                                                                                           | *long*                                                                                                                                                                                            | :heavy_minus_sign:                                                                                                                                                                                | The starting server knowledge.  If provided, only entities that have changed since `last_knowledge_of_server` will be included.                                                                   |

### Response

**[GetScheduledTransactionsResponse](../../Models/Requests/GetScheduledTransactionsResponse.md)**

### Errors

| Error Type                                    | Status Code                                   | Content Type                                  |
| --------------------------------------------- | --------------------------------------------- | --------------------------------------------- |
| WalkerTX.Ynab.SDK.Models.Errors.ErrorResponse | 404                                           | application/json                              |
| WalkerTX.Ynab.SDK.Models.Errors.ErrorResponse | default                                       | application/json                              |
| WalkerTX.Ynab.SDK.Models.Errors.APIException  | 4XX, 5XX                                      | \*/\*                                         |

## Create

Creates a single scheduled transaction (a transaction with a future date).

### Example Usage

<!-- UsageSnippet language="csharp" operationID="createScheduledTransaction" method="post" path="/budgets/{budget_id}/scheduled_transactions" -->
```csharp
using NodaTime;
using WalkerTX.Ynab.SDK;
using WalkerTX.Ynab.SDK.Models.Components;

var sdk = new Ynab(bearer: "<YOUR_BEARER_TOKEN_HERE>");

var res = await sdk.ScheduledTransactions.CreateAsync(
    budgetId: "<id>",
    postScheduledTransactionWrapper: new PostScheduledTransactionWrapper() {
        ScheduledTransaction = new SaveScheduledTransaction() {
            AccountId = "1cb7f54b-9ed5-48fd-8642-a56bd5ee2fca",
            Date = LocalDate.FromDateTime(System.DateTime.Parse("2024-04-15")),
        },
    }
);

// handle response
```

### Parameters

| Parameter                                                                                                                                                                                         | Type                                                                                                                                                                                              | Required                                                                                                                                                                                          | Description                                                                                                                                                                                       |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `BudgetId`                                                                                                                                                                                        | *string*                                                                                                                                                                                          | :heavy_check_mark:                                                                                                                                                                                | The id of the budget. "last-used" can be used to specify the last used budget and "default" can be used if default budget selection is enabled (see: https://api.ynab.com/#oauth-default-budget). |
| `PostScheduledTransactionWrapper`                                                                                                                                                                 | [PostScheduledTransactionWrapper](../../Models/Components/PostScheduledTransactionWrapper.md)                                                                                                     | :heavy_check_mark:                                                                                                                                                                                | The scheduled transaction to create                                                                                                                                                               |

### Response

**[CreateScheduledTransactionResponse](../../Models/Requests/CreateScheduledTransactionResponse.md)**

### Errors

| Error Type                                    | Status Code                                   | Content Type                                  |
| --------------------------------------------- | --------------------------------------------- | --------------------------------------------- |
| WalkerTX.Ynab.SDK.Models.Errors.ErrorResponse | 400                                           | application/json                              |
| WalkerTX.Ynab.SDK.Models.Errors.APIException  | 4XX, 5XX                                      | \*/\*                                         |

## Get

Returns a single scheduled transaction

### Example Usage

<!-- UsageSnippet language="csharp" operationID="getScheduledTransactionById" method="get" path="/budgets/{budget_id}/scheduled_transactions/{scheduled_transaction_id}" -->
```csharp
using WalkerTX.Ynab.SDK;
using WalkerTX.Ynab.SDK.Models.Components;

var sdk = new Ynab(bearer: "<YOUR_BEARER_TOKEN_HERE>");

var res = await sdk.ScheduledTransactions.GetAsync(
    budgetId: "<id>",
    scheduledTransactionId: "<id>"
);

// handle response
```

### Parameters

| Parameter                                                                                                                                                                                         | Type                                                                                                                                                                                              | Required                                                                                                                                                                                          | Description                                                                                                                                                                                       |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `BudgetId`                                                                                                                                                                                        | *string*                                                                                                                                                                                          | :heavy_check_mark:                                                                                                                                                                                | The id of the budget. "last-used" can be used to specify the last used budget and "default" can be used if default budget selection is enabled (see: https://api.ynab.com/#oauth-default-budget). |
| `ScheduledTransactionId`                                                                                                                                                                          | *string*                                                                                                                                                                                          | :heavy_check_mark:                                                                                                                                                                                | The id of the scheduled transaction                                                                                                                                                               |

### Response

**[GetScheduledTransactionByIdResponse](../../Models/Requests/GetScheduledTransactionByIdResponse.md)**

### Errors

| Error Type                                    | Status Code                                   | Content Type                                  |
| --------------------------------------------- | --------------------------------------------- | --------------------------------------------- |
| WalkerTX.Ynab.SDK.Models.Errors.ErrorResponse | 404                                           | application/json                              |
| WalkerTX.Ynab.SDK.Models.Errors.ErrorResponse | default                                       | application/json                              |
| WalkerTX.Ynab.SDK.Models.Errors.APIException  | 4XX, 5XX                                      | \*/\*                                         |

## Update

Updates a single scheduled transaction

### Example Usage

<!-- UsageSnippet language="csharp" operationID="updateScheduledTransaction" method="put" path="/budgets/{budget_id}/scheduled_transactions/{scheduled_transaction_id}" -->
```csharp
using NodaTime;
using WalkerTX.Ynab.SDK;
using WalkerTX.Ynab.SDK.Models.Components;

var sdk = new Ynab(bearer: "<YOUR_BEARER_TOKEN_HERE>");

var res = await sdk.ScheduledTransactions.UpdateAsync(
    budgetId: "<id>",
    scheduledTransactionId: "<id>",
    putScheduledTransactionWrapper: new PutScheduledTransactionWrapper() {
        ScheduledTransaction = new SaveScheduledTransaction() {
            AccountId = "8ca52c3e-66a2-43a1-82f1-fa05cadf8245",
            Date = LocalDate.FromDateTime(System.DateTime.Parse("2025-01-04")),
        },
    }
);

// handle response
```

### Parameters

| Parameter                                                                                                                                                                                         | Type                                                                                                                                                                                              | Required                                                                                                                                                                                          | Description                                                                                                                                                                                       |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `BudgetId`                                                                                                                                                                                        | *string*                                                                                                                                                                                          | :heavy_check_mark:                                                                                                                                                                                | The id of the budget. "last-used" can be used to specify the last used budget and "default" can be used if default budget selection is enabled (see: https://api.ynab.com/#oauth-default-budget). |
| `ScheduledTransactionId`                                                                                                                                                                          | *string*                                                                                                                                                                                          | :heavy_check_mark:                                                                                                                                                                                | The id of the scheduled transaction                                                                                                                                                               |
| `PutScheduledTransactionWrapper`                                                                                                                                                                  | [PutScheduledTransactionWrapper](../../Models/Components/PutScheduledTransactionWrapper.md)                                                                                                       | :heavy_check_mark:                                                                                                                                                                                | The scheduled transaction to update                                                                                                                                                               |

### Response

**[UpdateScheduledTransactionResponse](../../Models/Requests/UpdateScheduledTransactionResponse.md)**

### Errors

| Error Type                                    | Status Code                                   | Content Type                                  |
| --------------------------------------------- | --------------------------------------------- | --------------------------------------------- |
| WalkerTX.Ynab.SDK.Models.Errors.ErrorResponse | 400                                           | application/json                              |
| WalkerTX.Ynab.SDK.Models.Errors.APIException  | 4XX, 5XX                                      | \*/\*                                         |

## Delete

Deletes a scheduled transaction

### Example Usage

<!-- UsageSnippet language="csharp" operationID="deleteScheduledTransaction" method="delete" path="/budgets/{budget_id}/scheduled_transactions/{scheduled_transaction_id}" -->
```csharp
using WalkerTX.Ynab.SDK;
using WalkerTX.Ynab.SDK.Models.Components;

var sdk = new Ynab(bearer: "<YOUR_BEARER_TOKEN_HERE>");

var res = await sdk.ScheduledTransactions.DeleteAsync(
    budgetId: "<id>",
    scheduledTransactionId: "<id>"
);

// handle response
```

### Parameters

| Parameter                                                                                                                                                                                         | Type                                                                                                                                                                                              | Required                                                                                                                                                                                          | Description                                                                                                                                                                                       |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `BudgetId`                                                                                                                                                                                        | *string*                                                                                                                                                                                          | :heavy_check_mark:                                                                                                                                                                                | The id of the budget. "last-used" can be used to specify the last used budget and "default" can be used if default budget selection is enabled (see: https://api.ynab.com/#oauth-default-budget). |
| `ScheduledTransactionId`                                                                                                                                                                          | *string*                                                                                                                                                                                          | :heavy_check_mark:                                                                                                                                                                                | The id of the scheduled transaction                                                                                                                                                               |

### Response

**[DeleteScheduledTransactionResponse](../../Models/Requests/DeleteScheduledTransactionResponse.md)**

### Errors

| Error Type                                    | Status Code                                   | Content Type                                  |
| --------------------------------------------- | --------------------------------------------- | --------------------------------------------- |
| WalkerTX.Ynab.SDK.Models.Errors.ErrorResponse | 404                                           | application/json                              |
| WalkerTX.Ynab.SDK.Models.Errors.APIException  | 4XX, 5XX                                      | \*/\*                                         |