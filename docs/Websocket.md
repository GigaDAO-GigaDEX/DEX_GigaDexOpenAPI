# Websocket API Docs

## Websocket API rete limits and limitations

- The websocket api is still in active development and some deprecation is expected to have.
- All transactiosn are being sent with their slot number, so you can use that to check if the transaction and track the time of confirmation.
- All names are case senstive.
- The base endpoint is: `wss://gigadexwss-production.up.railway.app/`.
- currently when subscribing to a market, you will be getting all recent trades, orderbook and your open order updates, can't filter them yet.

## Subscribing to a websocket channel

```json
{
  "SUBSCRIBE": "USER",
  "UID": 1,
  "MARKET": "lootboxes"
}
```

Where the `MARKET` is the marketname that you want to subscribe to, always going to be lowerCase, and the `UID` is the user account id on the smart contract that you want to subscribe with.

## Unsubscribing from a websocket and switching markets

```json
{
  "UNSUBSCRIBE": "USER",
  "UID": 1,
  "MARKET": "lootboxes"
}
```

sending this message will unsubscribe you from that market, and can also subscribe you to another market by instantly following up with:

```json
{
  "MARKET": "lootboxes",
  "SUBSCRIBE": "USER",
  "UID": 1
}
```

## Message types

### Balanaces updates

```json
{
  "MARKET": "lootboxes",
  "MESSAGE": {
    "CLAIMABLE_BALANCE": [0, 0],
    "SLOT": 181429079
  }
}
```

### Market Orders

```json
{
  "MARKET": "lootboxes",
  "TRADES": ["price", "amount", false],
  "SLOT": "slot"
}
```

in which, it comes in an array [] of types [float, int, bool], where the bool is true if the trade is a buy, and false if it's a sell.
amounts are counted in lamports or whatever the smallest unit of the token is.

### Orderbook

```json
{
  "MARKET" : "lootboxes",
  {"ASKS": [[1, 1],[1, 1]], "BIDS": [[1, 1],[1, 1]]}
  "SLOT": 123456789
}
```

in which, it comes in an object {} with two keys, `ASKS` and `BIDS`, each of them is an array [] of types [float, int], where the float is the price, and the int is the amount, amounts are counted in lamports or whatever the smallest unit of the token is.

### Open orders

To be continued.
