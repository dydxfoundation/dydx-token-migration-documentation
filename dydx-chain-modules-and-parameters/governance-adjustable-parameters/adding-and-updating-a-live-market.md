# Adding & Updating a Live Market

## Adding a New Market

This functionality allows the community to add new market to dYdX Chain protocol software, which shall be done by including the following message in the governance proposal (in this particular order):

```
MsgCreateOracle (create objects in x/prices)
MsgCreatePerpetual (create object in x/perpetual)
MsgCreatePerpetualClobPair (create object in x/clob)
MsgDelayMessage (schedule a MsgSetClobPairStatus to enable trading in x/clob)
```

## Updating a Live Market

This functionality allows the community to update parameters of a live market, which can be composed of 4 parts:

### Liquidity Tiers

Liquidity Tier is updatable through `MsgSetLiquidityTier`.

### Market

The Prices module (x/prices) is updatable through `MsgUpdateMarketParam`.

### Perpetual

The Perpetual module (x/perpetuals) is updatable through `MsgUpdatePerpetual`.

### Clob

The Clob module (x/clob) is updatable through `MsgUpdateClobPair`.

\
