# API Reference Overview

[Home](https://github.com/cpayapi-com/document/blob/main/README.md) / 
_API Reference Overview_

## Table of Contents

- [API Host](#api-host)
- [APIs](#apis)
  - [Transaction API](#transaction-api)
  - [Account API](#account-api)
  - [KYC API](#kyc-api)
- [SDK](#sdk)
- [Postman Collection](#postman-collection)
- [Idempotency](#idempotency)


## API Host

The environments can be accessed via the API hosts below.

| Environment | API Host |
| :----  | :---- |
|production   | https://live.cpayapi.com |
|sandbox  | https://live.cpayapi.com |

## APIs
### Transaction API
- [Query Payment Transaction](https://github.com/cpayapi-com/document/blob/main/api-reference/query-payment-transaction.md)
- [Payin with H2H Mode(v1)](#)
- [Payin with H2H Mode(v2)](#)
### Account API
- [Query Account Balance](#)

### KYC API
- [Submit KYC Information](#)

## SDK
- [PHP SDK](#)
- [Golang SDK](#)
- [Java SDK](#)
> coming soon.

## Postman Collection
Download [here](#)

> coming soon.

## Idempotency
All APIs support idempotency, allowing to retry a request multiple times while only performing the action once. 
This helps avoid unwanted duplication in case of failures and retries.

If the process has not been completed in the previous request because of a transient error or timeout,
the subsequent retry pushes the action to its completion. 

If the process has been completed already, the retry process will be performed only once and get the same result.  

The following shows the most commonly used APIs and their idempotency rules.

| API Name | Rules |
| :----  | :---- |
|Payin with H2H Mode   | `merchantId` + `merchantTradeNo` |



