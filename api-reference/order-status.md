# Order Status

[Home](https://github.com/cpayapi-com/document/blob/main/README.md) /
[API Overview](https://github.com/cpayapi-com/document/blob/main/api-reference/overview.md) / 
_Order Status_


| Status | Description |
| :----  | :---- |
|0   | PENDING (Temporary status, the transaction may not be started in the bank side and it will be changed to 14/15 finally) |
|11  | PROCESSING (Temporary status, the transaction is waiting for a notification from the bank, it will be changed to 14/15 finally) |
|14  | COMPLETED (Final status, the transaction is successful)|
|15  | CLOSED (Final status, the transaction is failed) |

