# CPay Integration Tutorial

## Table of Contents

- [Introduction](#introduction)
- [Prerequisites](#prerequisites)
- [Merchant Portal](#merchant-portal)
- [How it Works](#how-it-works)
- [API Reference](#api-reference)
   - [APIs](#apis)
   - [API Host](#api-host)
   - [Signature](#signature)
   - [Error Code](#error-code)
   - [Order Status](#order-status)
- [Webhook Notification](#webhook-notification)
- [FAQ](#api-reference)
- [Change Log](#change-log)
- [Contacts](#contacts)


## Introduction
Welcome to the integration tutorial.  
In this tutorial, we will show details how best to finish the integration.


## Prerequisites
In this section, we will show the preparations before the integration.  
Especially, we suggest you should update the `Password`, don't leak `Password` and `Security Key` to others.

1. Provide Merchant Information  
   Merchant should provide the bellowing information to CPay team,
   - `Brand Name`
   - `Company Name`
   - `Website`
   - `Email`

2. Initialize Merchant Information  
   CPay team will initialize all information. After that, CPay team will send merchant the bellowing information,
   - `Username`
   - `Password`
   - Link of `Merchant Portal`

3. Change Password  
   Merchant login `Merchant Portal` and update the password firstly.
   Navigate to `User Center / User Center / Change Password`.
   > Important: Leaking `Password` to others is risky.


4. Get Credentials
   Navigate to `User Center / User Center / Basic Information`, 
   and merchant will get the bellowing information:
   - `Merchant ID`
   - `Security Key`
   - `API Host`

   > Important: Leaking `Security Key` to others is risky.

## Merchant Portal
In this section, we will show details how to use the `Merchant Portal` with a manual.

> Link https://console.cpayapi.com  
> See details [here](https://github.com/cpayapi-com/document/blob/main/merchant-portal/manual.md)


## How it works
In this section, we will show details how CPay systems work with the acquirer bank and our merchant.

> See details [here](https://github.com/cpayapi-com/document/blob/main/how-it-works.md)

## API Reference
In this section, we will show details of CPay APIs for technical engineer.


### APIs 
All APIs will be seen [here](https://github.com/cpayapi-com/document/blob/main/api-reference/overview.md)


### API Host
The environments can be accessed via the API hosts below.

| Environment | API Host |
| :----  | :---- |
|production | https://live.cpayapi.com |
|sandbox    | https://live.cpayapi.com |

### Signature
In this section, we will show the mechanism of generating parameter `sign`.  
We also provide some code examples to shorten integration time.

> See details [here](https://github.com/cpayapi-com/document/blob/main/api-reference/signature.md)


### Error Code
> See details [here](https://github.com/cpayapi-com/document/blob/main/api-reference/error-code.md)


### Order Status
> See details [here](https://github.com/cpayapi-com/document/blob/main/api-reference/order-status.md)


## Webhook Notification
In this section, we will show details how CPay webhook service works, including `Configuration`, `Retry Mechanism` and `Natification Demos`.

> See details [here](https://github.com/cpayapi-com/document/blob/main/webhook-notification.md)

## FAQ
In this section, we will show the frequently-asked questions about CPay service.

> See details [here](https://github.com/cpayapi-com/document/blob/main/faq.md)

## Change Log
In this section, we will show all history change logs of the document.

> See details [here](https://github.com/cpayapi-com/document/blob/main/change-log.md)


## Contacts
If you have any further questions or suggestions, please don't hesitate to reach out to us.

> Email: tech_support@cpayfinance.com

