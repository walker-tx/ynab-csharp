# Transactions
(*Transactions*)

## Overview

The transactions for a budget

### Available Operations

* [List](#list) - List transactions
* [Create](#create) - Create a single transaction or multiple transactions
* [UpdateMany](#updatemany) - Update multiple transactions
* [Import](#import) - Import transactions
* [Get](#get) - Single transaction
* [UpdateOne](#updateone) - Updates an existing transaction
* [Delete](#delete) - Deletes an existing transaction
* [ListByAccount](#listbyaccount) - List account transactions
* [ListByCategory](#listbycategory) - List category transactions, excluding any pending transactions
* [ListByPayee](#listbypayee) - List payee transactions, excluding any pending transactions
* [ListByMonth](#listbymonth) - List transactions in month, excluding any pending transactions

## List

Returns budget transactions, excluding any pending transactions

### Example Usage

<!-- UsageSnippet language="csharp" operationID="getTransactions" method="get" path="/budgets/{budget_id}/transactions" -->
```csharp
using WalkerTX.Ynab.SDK;
using WalkerTX.Ynab.SDK.Models.Components;

var sdk = new Ynab(bearer: "<YOUR_BEARER_TOKEN_HERE>");

var res = await sdk.Transactions.ListAsync(budgetId: "<id>");

// handle response
```

### Parameters

| Parameter                                                                                                                                                                                         | Type                                                                                                                                                                                              | Required                                                                                                                                                                                          | Description                                                                                                                                                                                       |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `BudgetId`                                                                                                                                                                                        | *string*                                                                                                                                                                                          | :heavy_check_mark:                                                                                                                                                                                | The id of the budget. "last-used" can be used to specify the last used budget and "default" can be used if default budget selection is enabled (see: https://api.ynab.com/#oauth-default-budget). |
| `SinceDate`                                                                                                                                                                                       | [LocalDate](https://nodatime.org/3.1.x/api/NodaTime.LocalDate.html)                                                                                                                               | :heavy_minus_sign:                                                                                                                                                                                | If specified, only transactions on or after this date will be included.  The date should be ISO formatted (e.g. 2016-12-30).                                                                      |
| `Type`                                                                                                                                                                                            | [GetTransactionsType](../../Models/Requests/GetTransactionsType.md)                                                                                                                               | :heavy_minus_sign:                                                                                                                                                                                | If specified, only transactions of the specified type will be included. "uncategorized" and "unapproved" are currently supported.                                                                 |
| `LastKnowledgeOfServer`                                                                                                                                                                           | *long*                                                                                                                                                                                            | :heavy_minus_sign:                                                                                                                                                                                | The starting server knowledge.  If provided, only entities that have changed since `last_knowledge_of_server` will be included.                                                                   |

### Response

**[GetTransactionsResponse](../../Models/Requests/GetTransactionsResponse.md)**

### Errors

| Error Type                                    | Status Code                                   | Content Type                                  |
| --------------------------------------------- | --------------------------------------------- | --------------------------------------------- |
| WalkerTX.Ynab.SDK.Models.Errors.ErrorResponse | 400, 404                                      | application/json                              |
| WalkerTX.Ynab.SDK.Models.Errors.APIException  | 4XX, 5XX                                      | \*/\*                                         |

## Create

Creates a single transaction or multiple transactions.  If you provide a body containing a `transaction` object, a single transaction will be created and if you provide a body containing a `transactions` array, multiple transactions will be created.  Scheduled transactions (transactions with a future date) cannot be created on this endpoint.

### Example Usage

<!-- UsageSnippet language="csharp" operationID="createTransaction" method="post" path="/budgets/{budget_id}/transactions" -->
```csharp
using WalkerTX.Ynab.SDK;
using WalkerTX.Ynab.SDK.Models.Components;

var sdk = new Ynab(bearer: "<YOUR_BEARER_TOKEN_HERE>");

var res = await sdk.Transactions.CreateAsync(
    budgetId: "<id>",
    postTransactionsWrapper: new PostTransactionsWrapper() {}
);

// handle response
```

### Parameters

| Parameter                                                                                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                                                                                  |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `BudgetId`                                                                                                                                                                                                                                                                                   | *string*                                                                                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                                                                                           | The id of the budget. "last-used" can be used to specify the last used budget and "default" can be used if default budget selection is enabled (see: https://api.ynab.com/#oauth-default-budget).                                                                                            |
| `PostTransactionsWrapper`                                                                                                                                                                                                                                                                    | [PostTransactionsWrapper](../../Models/Components/PostTransactionsWrapper.md)                                                                                                                                                                                                                | :heavy_check_mark:                                                                                                                                                                                                                                                                           | The transaction or transactions to create.  To create a single transaction you can specify a value for the `transaction` object and to create multiple transactions you can specify an array of `transactions`.  It is expected that you will only provide a value for one of these objects. |

### Response

**[CreateTransactionResponse](../../Models/Requests/CreateTransactionResponse.md)**

### Errors

| Error Type                                    | Status Code                                   | Content Type                                  |
| --------------------------------------------- | --------------------------------------------- | --------------------------------------------- |
| WalkerTX.Ynab.SDK.Models.Errors.ErrorResponse | 400, 409                                      | application/json                              |
| WalkerTX.Ynab.SDK.Models.Errors.APIException  | 4XX, 5XX                                      | \*/\*                                         |

## UpdateMany

Updates multiple transactions, by `id` or `import_id`.

### Example Usage

<!-- UsageSnippet language="csharp" operationID="updateTransactions" method="patch" path="/budgets/{budget_id}/transactions" -->
```csharp
using System.Collections.Generic;
using WalkerTX.Ynab.SDK;
using WalkerTX.Ynab.SDK.Models.Components;

var sdk = new Ynab(bearer: "<YOUR_BEARER_TOKEN_HERE>");

var res = await sdk.Transactions.UpdateManyAsync(
    budgetId: "<id>",
    patchTransactionsWrapper: new PatchTransactionsWrapper() {
        Transactions = new List<SaveTransactionWithIdOrImportId>() {
            new SaveTransactionWithIdOrImportId() {},
        },
    }
);

// handle response
```

### Parameters

| Parameter                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              | Type                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   | Required                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `BudgetId`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             | *string*                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               | :heavy_check_mark:                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     | The id of the budget. "last-used" can be used to specify the last used budget and "default" can be used if default budget selection is enabled (see: https://api.ynab.com/#oauth-default-budget).                                                                                                                                                                                                                                                                                                      |
| `PatchTransactionsWrapper`                                                                                                                                                                                                                                                                                                                                                                                                                                                                             | [PatchTransactionsWrapper](../../Models/Components/PatchTransactionsWrapper.md)                                                                                                                                                                                                                                                                                                                                                                                                                        | :heavy_check_mark:                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     | The transactions to update. Each transaction must have either an `id` or `import_id` specified. If `id` is specified as null an `import_id` value can be provided which will allow transaction(s) to be updated by its `import_id`. If an `id` is specified, it will always be used for lookup.  You should not specify both `id` and `import_id`.  Updating an `import_id` on an existing transaction is not allowed; if an `import_id` is specified, it will only be used to lookup the transaction. |

### Response

**[UpdateTransactionsResponse](../../Models/Requests/UpdateTransactionsResponse.md)**

### Errors

| Error Type                                    | Status Code                                   | Content Type                                  |
| --------------------------------------------- | --------------------------------------------- | --------------------------------------------- |
| WalkerTX.Ynab.SDK.Models.Errors.ErrorResponse | 400                                           | application/json                              |
| WalkerTX.Ynab.SDK.Models.Errors.APIException  | 4XX, 5XX                                      | \*/\*                                         |

## Import

Imports available transactions on all linked accounts for the given budget.  Linked accounts allow transactions to be imported directly from a specified financial institution and this endpoint initiates that import.  Sending a request to this endpoint is the equivalent of clicking "Import" on each account in the web application or tapping the "New Transactions" banner in the mobile applications.  The response for this endpoint contains the transaction ids that have been imported.

### Example Usage

<!-- UsageSnippet language="csharp" operationID="importTransactions" method="post" path="/budgets/{budget_id}/transactions/import" -->
```csharp
using WalkerTX.Ynab.SDK;
using WalkerTX.Ynab.SDK.Models.Components;

var sdk = new Ynab(bearer: "<YOUR_BEARER_TOKEN_HERE>");

var res = await sdk.Transactions.ImportAsync(budgetId: "<id>");

// handle response
```

### Parameters

| Parameter                                                                                                                                                                                         | Type                                                                                                                                                                                              | Required                                                                                                                                                                                          | Description                                                                                                                                                                                       |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `BudgetId`                                                                                                                                                                                        | *string*                                                                                                                                                                                          | :heavy_check_mark:                                                                                                                                                                                | The id of the budget. "last-used" can be used to specify the last used budget and "default" can be used if default budget selection is enabled (see: https://api.ynab.com/#oauth-default-budget). |

### Response

**[ImportTransactionsResponse](../../Models/Requests/ImportTransactionsResponse.md)**

### Errors

| Error Type                                    | Status Code                                   | Content Type                                  |
| --------------------------------------------- | --------------------------------------------- | --------------------------------------------- |
| WalkerTX.Ynab.SDK.Models.Errors.ErrorResponse | 400                                           | application/json                              |
| WalkerTX.Ynab.SDK.Models.Errors.APIException  | 4XX, 5XX                                      | \*/\*                                         |

## Get

Returns a single transaction

### Example Usage

<!-- UsageSnippet language="csharp" operationID="getTransactionById" method="get" path="/budgets/{budget_id}/transactions/{transaction_id}" -->
```csharp
using WalkerTX.Ynab.SDK;
using WalkerTX.Ynab.SDK.Models.Components;

var sdk = new Ynab(bearer: "<YOUR_BEARER_TOKEN_HERE>");

var res = await sdk.Transactions.GetAsync(
    budgetId: "<id>",
    transactionId: "<id>"
);

// handle response
```

### Parameters

| Parameter                                                                                                                                                                                         | Type                                                                                                                                                                                              | Required                                                                                                                                                                                          | Description                                                                                                                                                                                       |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `BudgetId`                                                                                                                                                                                        | *string*                                                                                                                                                                                          | :heavy_check_mark:                                                                                                                                                                                | The id of the budget. "last-used" can be used to specify the last used budget and "default" can be used if default budget selection is enabled (see: https://api.ynab.com/#oauth-default-budget). |
| `TransactionId`                                                                                                                                                                                   | *string*                                                                                                                                                                                          | :heavy_check_mark:                                                                                                                                                                                | The id of the transaction                                                                                                                                                                         |

### Response

**[GetTransactionByIdResponse](../../Models/Requests/GetTransactionByIdResponse.md)**

### Errors

| Error Type                                    | Status Code                                   | Content Type                                  |
| --------------------------------------------- | --------------------------------------------- | --------------------------------------------- |
| WalkerTX.Ynab.SDK.Models.Errors.ErrorResponse | 404                                           | application/json                              |
| WalkerTX.Ynab.SDK.Models.Errors.ErrorResponse | default                                       | application/json                              |
| WalkerTX.Ynab.SDK.Models.Errors.APIException  | 4XX, 5XX                                      | \*/\*                                         |

## UpdateOne

Updates a single transaction

### Example Usage

<!-- UsageSnippet language="csharp" operationID="updateTransaction" method="put" path="/budgets/{budget_id}/transactions/{transaction_id}" -->
```csharp
using WalkerTX.Ynab.SDK;
using WalkerTX.Ynab.SDK.Models.Components;

var sdk = new Ynab(bearer: "<YOUR_BEARER_TOKEN_HERE>");

var res = await sdk.Transactions.UpdateOneAsync(
    budgetId: "<id>",
    transactionId: "<id>",
    putTransactionWrapper: new PutTransactionWrapper() {
        Transaction = new ExistingTransaction() {},
    }
);

// handle response
```

### Parameters

| Parameter                                                                                                                                                                                         | Type                                                                                                                                                                                              | Required                                                                                                                                                                                          | Description                                                                                                                                                                                       |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `BudgetId`                                                                                                                                                                                        | *string*                                                                                                                                                                                          | :heavy_check_mark:                                                                                                                                                                                | The id of the budget. "last-used" can be used to specify the last used budget and "default" can be used if default budget selection is enabled (see: https://api.ynab.com/#oauth-default-budget). |
| `TransactionId`                                                                                                                                                                                   | *string*                                                                                                                                                                                          | :heavy_check_mark:                                                                                                                                                                                | The id of the transaction                                                                                                                                                                         |
| `PutTransactionWrapper`                                                                                                                                                                           | [PutTransactionWrapper](../../Models/Components/PutTransactionWrapper.md)                                                                                                                         | :heavy_check_mark:                                                                                                                                                                                | The transaction to update                                                                                                                                                                         |

### Response

**[UpdateTransactionResponse](../../Models/Requests/UpdateTransactionResponse.md)**

### Errors

| Error Type                                    | Status Code                                   | Content Type                                  |
| --------------------------------------------- | --------------------------------------------- | --------------------------------------------- |
| WalkerTX.Ynab.SDK.Models.Errors.ErrorResponse | 400                                           | application/json                              |
| WalkerTX.Ynab.SDK.Models.Errors.APIException  | 4XX, 5XX                                      | \*/\*                                         |

## Delete

Deletes a transaction

### Example Usage

<!-- UsageSnippet language="csharp" operationID="deleteTransaction" method="delete" path="/budgets/{budget_id}/transactions/{transaction_id}" -->
```csharp
using WalkerTX.Ynab.SDK;
using WalkerTX.Ynab.SDK.Models.Components;

var sdk = new Ynab(bearer: "<YOUR_BEARER_TOKEN_HERE>");

var res = await sdk.Transactions.DeleteAsync(
    budgetId: "<id>",
    transactionId: "<id>"
);

// handle response
```

### Parameters

| Parameter                                                                                                                                                                                         | Type                                                                                                                                                                                              | Required                                                                                                                                                                                          | Description                                                                                                                                                                                       |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `BudgetId`                                                                                                                                                                                        | *string*                                                                                                                                                                                          | :heavy_check_mark:                                                                                                                                                                                | The id of the budget. "last-used" can be used to specify the last used budget and "default" can be used if default budget selection is enabled (see: https://api.ynab.com/#oauth-default-budget). |
| `TransactionId`                                                                                                                                                                                   | *string*                                                                                                                                                                                          | :heavy_check_mark:                                                                                                                                                                                | The id of the transaction                                                                                                                                                                         |

### Response

**[DeleteTransactionResponse](../../Models/Requests/DeleteTransactionResponse.md)**

### Errors

| Error Type                                    | Status Code                                   | Content Type                                  |
| --------------------------------------------- | --------------------------------------------- | --------------------------------------------- |
| WalkerTX.Ynab.SDK.Models.Errors.ErrorResponse | 404                                           | application/json                              |
| WalkerTX.Ynab.SDK.Models.Errors.APIException  | 4XX, 5XX                                      | \*/\*                                         |

## ListByAccount

Returns all transactions for a specified account, excluding any pending transactions

### Example Usage

<!-- UsageSnippet language="csharp" operationID="getTransactionsByAccount" method="get" path="/budgets/{budget_id}/accounts/{account_id}/transactions" -->
```csharp
using WalkerTX.Ynab.SDK;
using WalkerTX.Ynab.SDK.Models.Components;
using WalkerTX.Ynab.SDK.Models.Requests;

var sdk = new Ynab(bearer: "<YOUR_BEARER_TOKEN_HERE>");

GetTransactionsByAccountRequest req = new GetTransactionsByAccountRequest() {
    BudgetId = "<id>",
    AccountId = "<id>",
};

var res = await sdk.Transactions.ListByAccountAsync(req);

// handle response
```

### Parameters

| Parameter                                                                                   | Type                                                                                        | Required                                                                                    | Description                                                                                 |
| ------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------- |
| `request`                                                                                   | [GetTransactionsByAccountRequest](../../Models/Requests/GetTransactionsByAccountRequest.md) | :heavy_check_mark:                                                                          | The request object to use for the request.                                                  |

### Response

**[GetTransactionsByAccountResponse](../../Models/Requests/GetTransactionsByAccountResponse.md)**

### Errors

| Error Type                                    | Status Code                                   | Content Type                                  |
| --------------------------------------------- | --------------------------------------------- | --------------------------------------------- |
| WalkerTX.Ynab.SDK.Models.Errors.ErrorResponse | 404                                           | application/json                              |
| WalkerTX.Ynab.SDK.Models.Errors.ErrorResponse | default                                       | application/json                              |
| WalkerTX.Ynab.SDK.Models.Errors.APIException  | 4XX, 5XX                                      | \*/\*                                         |

## ListByCategory

Returns all transactions for a specified category

### Example Usage

<!-- UsageSnippet language="csharp" operationID="getTransactionsByCategory" method="get" path="/budgets/{budget_id}/categories/{category_id}/transactions" -->
```csharp
using WalkerTX.Ynab.SDK;
using WalkerTX.Ynab.SDK.Models.Components;
using WalkerTX.Ynab.SDK.Models.Requests;

var sdk = new Ynab(bearer: "<YOUR_BEARER_TOKEN_HERE>");

GetTransactionsByCategoryRequest req = new GetTransactionsByCategoryRequest() {
    BudgetId = "<id>",
    CategoryId = "<id>",
};

var res = await sdk.Transactions.ListByCategoryAsync(req);

// handle response
```

### Parameters

| Parameter                                                                                     | Type                                                                                          | Required                                                                                      | Description                                                                                   |
| --------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------- |
| `request`                                                                                     | [GetTransactionsByCategoryRequest](../../Models/Requests/GetTransactionsByCategoryRequest.md) | :heavy_check_mark:                                                                            | The request object to use for the request.                                                    |

### Response

**[GetTransactionsByCategoryResponse](../../Models/Requests/GetTransactionsByCategoryResponse.md)**

### Errors

| Error Type                                    | Status Code                                   | Content Type                                  |
| --------------------------------------------- | --------------------------------------------- | --------------------------------------------- |
| WalkerTX.Ynab.SDK.Models.Errors.ErrorResponse | 404                                           | application/json                              |
| WalkerTX.Ynab.SDK.Models.Errors.ErrorResponse | default                                       | application/json                              |
| WalkerTX.Ynab.SDK.Models.Errors.APIException  | 4XX, 5XX                                      | \*/\*                                         |

## ListByPayee

Returns all transactions for a specified payee

### Example Usage

<!-- UsageSnippet language="csharp" operationID="getTransactionsByPayee" method="get" path="/budgets/{budget_id}/payees/{payee_id}/transactions" -->
```csharp
using WalkerTX.Ynab.SDK;
using WalkerTX.Ynab.SDK.Models.Components;
using WalkerTX.Ynab.SDK.Models.Requests;

var sdk = new Ynab(bearer: "<YOUR_BEARER_TOKEN_HERE>");

GetTransactionsByPayeeRequest req = new GetTransactionsByPayeeRequest() {
    BudgetId = "<id>",
    PayeeId = "<id>",
};

var res = await sdk.Transactions.ListByPayeeAsync(req);

// handle response
```

### Parameters

| Parameter                                                                               | Type                                                                                    | Required                                                                                | Description                                                                             |
| --------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------- |
| `request`                                                                               | [GetTransactionsByPayeeRequest](../../Models/Requests/GetTransactionsByPayeeRequest.md) | :heavy_check_mark:                                                                      | The request object to use for the request.                                              |

### Response

**[GetTransactionsByPayeeResponse](../../Models/Requests/GetTransactionsByPayeeResponse.md)**

### Errors

| Error Type                                    | Status Code                                   | Content Type                                  |
| --------------------------------------------- | --------------------------------------------- | --------------------------------------------- |
| WalkerTX.Ynab.SDK.Models.Errors.ErrorResponse | 404                                           | application/json                              |
| WalkerTX.Ynab.SDK.Models.Errors.ErrorResponse | default                                       | application/json                              |
| WalkerTX.Ynab.SDK.Models.Errors.APIException  | 4XX, 5XX                                      | \*/\*                                         |

## ListByMonth

Returns all transactions for a specified month

### Example Usage

<!-- UsageSnippet language="csharp" operationID="getTransactionsByMonth" method="get" path="/budgets/{budget_id}/months/{month}/transactions" -->
```csharp
using WalkerTX.Ynab.SDK;
using WalkerTX.Ynab.SDK.Models.Components;
using WalkerTX.Ynab.SDK.Models.Requests;

var sdk = new Ynab(bearer: "<YOUR_BEARER_TOKEN_HERE>");

GetTransactionsByMonthRequest req = new GetTransactionsByMonthRequest() {
    BudgetId = "<id>",
    Month = "<value>",
};

var res = await sdk.Transactions.ListByMonthAsync(req);

// handle response
```

### Parameters

| Parameter                                                                               | Type                                                                                    | Required                                                                                | Description                                                                             |
| --------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------- |
| `request`                                                                               | [GetTransactionsByMonthRequest](../../Models/Requests/GetTransactionsByMonthRequest.md) | :heavy_check_mark:                                                                      | The request object to use for the request.                                              |

### Response

**[GetTransactionsByMonthResponse](../../Models/Requests/GetTransactionsByMonthResponse.md)**

### Errors

| Error Type                                    | Status Code                                   | Content Type                                  |
| --------------------------------------------- | --------------------------------------------- | --------------------------------------------- |
| WalkerTX.Ynab.SDK.Models.Errors.ErrorResponse | 404                                           | application/json                              |
| WalkerTX.Ynab.SDK.Models.Errors.ErrorResponse | default                                       | application/json                              |
| WalkerTX.Ynab.SDK.Models.Errors.APIException  | 4XX, 5XX                                      | \*/\*                                         |