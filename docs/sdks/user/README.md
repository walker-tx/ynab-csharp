# User
(*User*)

## Overview

### Available Operations

* [Get](#get) - User info

## Get

Returns authenticated user information

### Example Usage

<!-- UsageSnippet language="csharp" operationID="getUser" method="get" path="/user" -->
```csharp
using WalkerTX.Ynab.SDK;
using WalkerTX.Ynab.SDK.Models.Components;

var sdk = new Ynab(bearer: "<YOUR_BEARER_TOKEN_HERE>");

var res = await sdk.User.GetAsync();

// handle response
```

### Response

**[GetUserResponse](../../Models/Requests/GetUserResponse.md)**

### Errors

| Error Type                                    | Status Code                                   | Content Type                                  |
| --------------------------------------------- | --------------------------------------------- | --------------------------------------------- |
| WalkerTX.Ynab.SDK.Models.Errors.ErrorResponse | default                                       | application/json                              |
| WalkerTX.Ynab.SDK.Models.Errors.APIException  | 4XX, 5XX                                      | \*/\*                                         |