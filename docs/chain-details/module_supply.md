### `supply` module

### Introduction

The `supply` module is responsible for retrieve total and liquid supply. 



### Queries

#### `query supply liquid` - Check the total supply of coins of the chain

We can also use  `query` command of the `supply` module to check the current total supply:

```json
$ cronosd query supply total
    {
    "supply": [
        {
        "denom": "basetcro",
        "amount": "[total_supply_amount]"
        }
    ]
    }
```

#### `query supply liquid` - Check the liquid supply of coins of the chain

We can also query the liquid supply, which is the total supply bonded subtracted by the non-circulating supply such as bonded amount, unvested amounts, and uncollected reward etc.

```json
$ cronosd query supply total
    {
    "supply": [
        {
        "denom": "basetcro",
        "amount": "[total_circulating_amount]"
        }
    ]
    }
```
