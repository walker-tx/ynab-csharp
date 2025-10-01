# Categories
(*Categories*)

## Overview

The categories for a budget

### Available Operations

* [List](#list) - List categories
* [Get](#get) - Single category
* [Update](#update) - Update a category
* [GetByMonth](#getbymonth) - Single category for a specific budget month
* [UpdateMonth](#updatemonth) - Update a category for a specific month

## List

Returns all categories grouped by category group.  Amounts (budgeted, activity, balance, etc.) are specific to the current budget month (UTC).

### Example Usage

<!-- UsageSnippet language="csharp" operationID="getCategories" method="get" path="/budgets/{budget_id}/categories" -->
```csharp
using WalkerTX.Ynab.SDK;
using WalkerTX.Ynab.SDK.Models.Components;

var sdk = new Ynab(bearer: "<YOUR_BEARER_TOKEN_HERE>");

var res = await sdk.Categories.ListAsync(budgetId: "<id>");

// handle response
```

### Parameters

| Parameter                                                                                                                                                                                         | Type                                                                                                                                                                                              | Required                                                                                                                                                                                          | Description                                                                                                                                                                                       |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `BudgetId`                                                                                                                                                                                        | *string*                                                                                                                                                                                          | :heavy_check_mark:                                                                                                                                                                                | The id of the budget. "last-used" can be used to specify the last used budget and "default" can be used if default budget selection is enabled (see: https://api.ynab.com/#oauth-default-budget). |
| `LastKnowledgeOfServer`                                                                                                                                                                           | *long*                                                                                                                                                                                            | :heavy_minus_sign:                                                                                                                                                                                | The starting server knowledge.  If provided, only entities that have changed since `last_knowledge_of_server` will be included.                                                                   |

### Response

**[GetCategoriesResponse](../../Models/Requests/GetCategoriesResponse.md)**

### Errors

| Error Type                                    | Status Code                                   | Content Type                                  |
| --------------------------------------------- | --------------------------------------------- | --------------------------------------------- |
| WalkerTX.Ynab.SDK.Models.Errors.ErrorResponse | 404                                           | application/json                              |
| WalkerTX.Ynab.SDK.Models.Errors.ErrorResponse | default                                       | application/json                              |
| WalkerTX.Ynab.SDK.Models.Errors.APIException  | 4XX, 5XX                                      | \*/\*                                         |

## Get

Returns a single category.  Amounts (budgeted, activity, balance, etc.) are specific to the current budget month (UTC).

### Example Usage

<!-- UsageSnippet language="csharp" operationID="getCategoryById" method="get" path="/budgets/{budget_id}/categories/{category_id}" -->
```csharp
using WalkerTX.Ynab.SDK;
using WalkerTX.Ynab.SDK.Models.Components;

var sdk = new Ynab(bearer: "<YOUR_BEARER_TOKEN_HERE>");

var res = await sdk.Categories.GetAsync(
    budgetId: "<id>",
    categoryId: "<id>"
);

// handle response
```

### Parameters

| Parameter                                                                                                                                                                                         | Type                                                                                                                                                                                              | Required                                                                                                                                                                                          | Description                                                                                                                                                                                       |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `BudgetId`                                                                                                                                                                                        | *string*                                                                                                                                                                                          | :heavy_check_mark:                                                                                                                                                                                | The id of the budget. "last-used" can be used to specify the last used budget and "default" can be used if default budget selection is enabled (see: https://api.ynab.com/#oauth-default-budget). |
| `CategoryId`                                                                                                                                                                                      | *string*                                                                                                                                                                                          | :heavy_check_mark:                                                                                                                                                                                | The id of the category                                                                                                                                                                            |

### Response

**[GetCategoryByIdResponse](../../Models/Requests/GetCategoryByIdResponse.md)**

### Errors

| Error Type                                    | Status Code                                   | Content Type                                  |
| --------------------------------------------- | --------------------------------------------- | --------------------------------------------- |
| WalkerTX.Ynab.SDK.Models.Errors.ErrorResponse | 404                                           | application/json                              |
| WalkerTX.Ynab.SDK.Models.Errors.ErrorResponse | default                                       | application/json                              |
| WalkerTX.Ynab.SDK.Models.Errors.APIException  | 4XX, 5XX                                      | \*/\*                                         |

## Update

Update a category

### Example Usage

<!-- UsageSnippet language="csharp" operationID="updateCategory" method="patch" path="/budgets/{budget_id}/categories/{category_id}" -->
```csharp
using WalkerTX.Ynab.SDK;
using WalkerTX.Ynab.SDK.Models.Components;

var sdk = new Ynab(bearer: "<YOUR_BEARER_TOKEN_HERE>");

var res = await sdk.Categories.UpdateAsync(
    budgetId: "<id>",
    categoryId: "<id>",
    patchCategoryWrapper: new PatchCategoryWrapper() {
        Category = new SaveCategory() {},
    }
);

// handle response
```

### Parameters

| Parameter                                                                                                                                                                                         | Type                                                                                                                                                                                              | Required                                                                                                                                                                                          | Description                                                                                                                                                                                       |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `BudgetId`                                                                                                                                                                                        | *string*                                                                                                                                                                                          | :heavy_check_mark:                                                                                                                                                                                | The id of the budget. "last-used" can be used to specify the last used budget and "default" can be used if default budget selection is enabled (see: https://api.ynab.com/#oauth-default-budget). |
| `CategoryId`                                                                                                                                                                                      | *string*                                                                                                                                                                                          | :heavy_check_mark:                                                                                                                                                                                | The id of the category                                                                                                                                                                            |
| `PatchCategoryWrapper`                                                                                                                                                                            | [PatchCategoryWrapper](../../Models/Components/PatchCategoryWrapper.md)                                                                                                                           | :heavy_check_mark:                                                                                                                                                                                | The category to update                                                                                                                                                                            |

### Response

**[UpdateCategoryResponse](../../Models/Requests/UpdateCategoryResponse.md)**

### Errors

| Error Type                                    | Status Code                                   | Content Type                                  |
| --------------------------------------------- | --------------------------------------------- | --------------------------------------------- |
| WalkerTX.Ynab.SDK.Models.Errors.ErrorResponse | 400                                           | application/json                              |
| WalkerTX.Ynab.SDK.Models.Errors.APIException  | 4XX, 5XX                                      | \*/\*                                         |

## GetByMonth

Returns a single category for a specific budget month.  Amounts (budgeted, activity, balance, etc.) are specific to the current budget month (UTC).

### Example Usage

<!-- UsageSnippet language="csharp" operationID="getMonthCategoryById" method="get" path="/budgets/{budget_id}/months/{month}/categories/{category_id}" -->
```csharp
using NodaTime;
using WalkerTX.Ynab.SDK;
using WalkerTX.Ynab.SDK.Models.Components;

var sdk = new Ynab(bearer: "<YOUR_BEARER_TOKEN_HERE>");

var res = await sdk.Categories.GetByMonthAsync(
    budgetId: "<id>",
    month: LocalDate.FromDateTime(System.DateTime.Parse("2025-10-27")),
    categoryId: "<id>"
);

// handle response
```

### Parameters

| Parameter                                                                                                                                                                                         | Type                                                                                                                                                                                              | Required                                                                                                                                                                                          | Description                                                                                                                                                                                       |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `BudgetId`                                                                                                                                                                                        | *string*                                                                                                                                                                                          | :heavy_check_mark:                                                                                                                                                                                | The id of the budget. "last-used" can be used to specify the last used budget and "default" can be used if default budget selection is enabled (see: https://api.ynab.com/#oauth-default-budget). |
| `Month`                                                                                                                                                                                           | [LocalDate](https://nodatime.org/3.1.x/api/NodaTime.LocalDate.html)                                                                                                                               | :heavy_check_mark:                                                                                                                                                                                | The budget month in ISO format (e.g. 2016-12-01) ("current" can also be used to specify the current calendar month (UTC))                                                                         |
| `CategoryId`                                                                                                                                                                                      | *string*                                                                                                                                                                                          | :heavy_check_mark:                                                                                                                                                                                | The id of the category                                                                                                                                                                            |

### Response

**[GetMonthCategoryByIdResponse](../../Models/Requests/GetMonthCategoryByIdResponse.md)**

### Errors

| Error Type                                    | Status Code                                   | Content Type                                  |
| --------------------------------------------- | --------------------------------------------- | --------------------------------------------- |
| WalkerTX.Ynab.SDK.Models.Errors.ErrorResponse | 404                                           | application/json                              |
| WalkerTX.Ynab.SDK.Models.Errors.ErrorResponse | default                                       | application/json                              |
| WalkerTX.Ynab.SDK.Models.Errors.APIException  | 4XX, 5XX                                      | \*/\*                                         |

## UpdateMonth

Update a category for a specific month.  Only `budgeted` amount can be updated.

### Example Usage

<!-- UsageSnippet language="csharp" operationID="updateMonthCategory" method="patch" path="/budgets/{budget_id}/months/{month}/categories/{category_id}" -->
```csharp
using NodaTime;
using WalkerTX.Ynab.SDK;
using WalkerTX.Ynab.SDK.Models.Components;

var sdk = new Ynab(bearer: "<YOUR_BEARER_TOKEN_HERE>");

var res = await sdk.Categories.UpdateMonthAsync(
    budgetId: "<id>",
    month: LocalDate.FromDateTime(System.DateTime.Parse("2023-01-08")),
    categoryId: "<id>",
    patchMonthCategoryWrapper: new PatchMonthCategoryWrapper() {
        Category = new SaveMonthCategory() {
            Budgeted = 147664,
        },
    }
);

// handle response
```

### Parameters

| Parameter                                                                                                                                                                                         | Type                                                                                                                                                                                              | Required                                                                                                                                                                                          | Description                                                                                                                                                                                       |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `BudgetId`                                                                                                                                                                                        | *string*                                                                                                                                                                                          | :heavy_check_mark:                                                                                                                                                                                | The id of the budget. "last-used" can be used to specify the last used budget and "default" can be used if default budget selection is enabled (see: https://api.ynab.com/#oauth-default-budget). |
| `Month`                                                                                                                                                                                           | [LocalDate](https://nodatime.org/3.1.x/api/NodaTime.LocalDate.html)                                                                                                                               | :heavy_check_mark:                                                                                                                                                                                | The budget month in ISO format (e.g. 2016-12-01) ("current" can also be used to specify the current calendar month (UTC))                                                                         |
| `CategoryId`                                                                                                                                                                                      | *string*                                                                                                                                                                                          | :heavy_check_mark:                                                                                                                                                                                | The id of the category                                                                                                                                                                            |
| `PatchMonthCategoryWrapper`                                                                                                                                                                       | [PatchMonthCategoryWrapper](../../Models/Components/PatchMonthCategoryWrapper.md)                                                                                                                 | :heavy_check_mark:                                                                                                                                                                                | The category to update.  Only `budgeted` amount can be updated and any other fields specified will be ignored.                                                                                    |

### Response

**[UpdateMonthCategoryResponse](../../Models/Requests/UpdateMonthCategoryResponse.md)**

### Errors

| Error Type                                    | Status Code                                   | Content Type                                  |
| --------------------------------------------- | --------------------------------------------- | --------------------------------------------- |
| WalkerTX.Ynab.SDK.Models.Errors.ErrorResponse | 400                                           | application/json                              |
| WalkerTX.Ynab.SDK.Models.Errors.APIException  | 4XX, 5XX                                      | \*/\*                                         |