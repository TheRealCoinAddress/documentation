# CoinAddress API Documentation

The API consists of 2 parts.

- Part one is the Swagger endpoint to perform deposits and withdawals https://test-api.coinaddress.io/swagger/index.html
- Part 2 is the callback flow, that is described below


## Callback types. 

Callback URLs are configured in the backoffice. You can have up to 3 callback URLs per project.

### Deposit Callback

Deposit callback is triggered when a transaction has 1 confirmation on the blockchain and then after 3 and 6 confirmations for BTC.

The callback structure is like this:

```
{
    "id": transaction_string_id,
    "type": "deposit",
    "crypto_address": {
        "id": address_string_id,
        "currency": "BTC",
        "address": "39mFf3X46YzUtfdwVQpYXPCMydc74ccbAZ",
        "foreign_id": "user-id:2048",
        "tag": null
    },
    "currency_sent": {
        "currency": "BTC",
        "amount": "6.53157512"
    },
    "currency_received": {
        "currency": "BTC",
        "amount": "6.53157512",
        "amount_minus_fee": "6.5119800"
    },
    "transactions": [
        {
            "id": string_transaction_id,
            "currency": "BTC",
            "address": "39mFf3X46YzUtfdwVQpYXPCMydc74ccbAZ",
            "tag": null,
            "amount": "6.53157512",
            "txid": "3950ad8149421a850d01dff88f024810e363ac18c9e8dd9bc0b9116e7937ad93",
            "confirmations": 3
        }
    ],
    "fees": [
        {
            "type": "deposit",
            "currency": "BTC",
            "amount": "0.01959472"
        }
    ],
    "error": "",
    "status": "confirmed"
}
```

### Withdrawal Callback

Withdrawal callback is triggered when transaction is sent to the blockchain (with 0 confirmations). Then it is triggered again with 1 confirmation and then with 3 and 6 confirmations. 

```
{
    "id": string_transaction_id,
    "foreign_id": "10",
    "type": "withdrawal",
    "crypto_address": {
        "id": 1,
        "currency": "BTC",
        "address": "115Mn1jCjBh1CNqug7yAB21Hq2rw8PfmTA",
        "tag": null
    },
    "currency_sent": {
        "currency": "BTC",
        "amount": "0.02000000"
    },
    "currency_received": {
        "currency": "BTC",
        "amount": "0.02000000"
    },
    "transactions": [
        {
            "id": 1,
            "currency": "BTC",
            "type": "withdrawal",
            "address": "115Mn1jCjBh1CNqug7yAB21Hq2rw8PfmTA",
            "tag": null,
            "amount": "0.02",
            "txid": "bb040d895ef7141ea0b06b04227d8f5dd4ee12d5b890e6e5633f6439393a666b",
            "confirmations": 3
        }
    ],
    "fees": [
        {
            "type": "mining",
            "currency": "BTC",
            "amount": "0.00007402"
        },
        {
            "type": "withdrawal",
            "currency": "BTC",
            "amount": "0.00002000"
        }
    ],
    "error": "",
    "status": "confirmed"
}
```