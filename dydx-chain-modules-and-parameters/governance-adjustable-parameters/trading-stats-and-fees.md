# Trading Stats and Fees

## Stats Module

The Stats Module tracks user maker and taker volumes over a period of time (aka look-back window). This is currently set to 30 days. The maker and taker volume info is used to place users in corresponding fee-tiers.

| Title                                                                                                                                      | Value                                    | Definition                                             |
| ------------------------------------------------------------------------------------------------------------------------------------------ | ---------------------------------------- | ------------------------------------------------------ |
| [window\_duration](https://github.com/dydxopsdao/networks/blob/fd7ee6e63e7e4b3ffab4fe600ac7cdb77c28d88d/dydx-mainnet-1/genesis.json#L3794) | <p>2592000s</p><p><br></p><p>30 days</p> | The desired number of seconds in the look-back window. |

## Fee Tiers Module

The current fee tier structure on dYdX Chain was developed to stimulate liquidity, incentivize traders with substantial volume and contribute to the platform's overall growth and competitiveness as it transitions from dYdX Layer 2 Protocol built on Ethereum to the dYdX Chain.

The fee tier structure has the following characteristics:

1. different fees for either maker or taker,
2. fee discounts based on each user’s 30 days trading volume across sub accounts and markets, and
3. uniform fee structure across all markets.

| Tier                                                                                                                              | <p>Absolute_volume_requirement</p><p>[30 day Trailing Volume]</p> | <p>Total_volume_share_requirement_ppm</p><p>[Exchange Market Share]</p> | <p>Maker_volume_share_requirement_ppm</p><p>[Maker Market Share]</p> | <p>maker_fee_ppm</p><p>[Maker Fee (bps)]</p> | <p>Taker_fee_ppm</p><p>[Taker Fee (bps)]</p> |
| --------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------- | ----------------------------------------------------------------------- | -------------------------------------------------------------------- | -------------------------------------------- | -------------------------------------------- |
| [1](https://github.com/dydxopsdao/networks/blob/fd7ee6e63e7e4b3ffab4fe600ac7cdb77c28d88d/dydx-mainnet-1/genesis.json#L1061-L1066) | 0 \[< $1M]                                                        | 0 \[-]                                                                  | 0 \[-]                                                               | 100 \[1.0]                                   | 500 \[5.0]                                   |
| [2](https://github.com/dydxopsdao/networks/blob/fd7ee6e63e7e4b3ffab4fe600ac7cdb77c28d88d/dydx-mainnet-1/genesis.json#L1069-L1074) | 1000000000000 \[≥ $1M]                                            | 0 \[-]                                                                  | 0 \[-]                                                               | 100 \[1.0]                                   | 450 \[4.5]                                   |
| [3](https://github.com/dydxopsdao/networks/blob/fd7ee6e63e7e4b3ffab4fe600ac7cdb77c28d88d/dydx-mainnet-1/genesis.json#L1077-L1082) | 5000000000000 \[≥ $5M]                                            | 0 \[-]                                                                  | 0 \[-]                                                               | 50 \[0.5]                                    | 400 \[4.0]                                   |
| [4](https://github.com/dydxopsdao/networks/blob/fd7ee6e63e7e4b3ffab4fe600ac7cdb77c28d88d/dydx-mainnet-1/genesis.json#L1085-L1090) | 25000000000000 \[≥ $25M]                                          | 0 \[-]                                                                  | 0 \[-]                                                               | 0 \[-]                                       | 350 \[3.5]                                   |
| [5](https://github.com/dydxopsdao/networks/blob/fd7ee6e63e7e4b3ffab4fe600ac7cdb77c28d88d/dydx-mainnet-1/genesis.json#L1093-L1098) | 125000000000000 \[≥ $125M]                                        | 0 \[-]                                                                  | 0 \[-]                                                               | 0 \[-]                                       | 300 \[3.0]                                   |
| [6](https://github.com/dydxopsdao/networks/blob/fd7ee6e63e7e4b3ffab4fe600ac7cdb77c28d88d/dydx-mainnet-1/genesis.json#L1101-L1106) | 125000000000000 \[≥ $125M]                                        | 5000 \[≥ 0.5%]                                                          | 0 \[-]                                                               | -50 \[-0.5]                                  | 250 \[2.5]                                   |
| [7](https://github.com/dydxopsdao/networks/blob/fd7ee6e63e7e4b3ffab4fe600ac7cdb77c28d88d/dydx-mainnet-1/genesis.json#L1109-L1114) | 125000000000000 \[≥ $125M]                                        | 5000 \[≥ 0.5%]                                                          | 10000 \[≥ 1%]                                                        | -70 \[-0.7]                                  | 250 \[2.5]                                   |
| [8](https://github.com/dydxopsdao/networks/blob/fd7ee6e63e7e4b3ffab4fe600ac7cdb77c28d88d/dydx-mainnet-1/genesis.json#L1117-L1122) | 125000000000000 \[≥ $125M]                                        | 5000 \[≥ 0.5%]                                                          | 20000 \[≥ 2%]                                                        | -90 \[-0.9]                                  | 250 \[2.5]                                   |
| [9](https://github.com/dydxopsdao/networks/blob/fd7ee6e63e7e4b3ffab4fe600ac7cdb77c28d88d/dydx-mainnet-1/genesis.json#L1125-L1130) | 125000000000000 \[≥ $125M]                                        | 5000 \[≥ 0.5%]                                                          | 40000 \[≥ 4%]                                                        | -110 \[-1.1]                                 | 250 \[2.5]                                   |

This fee tier w [implemented](https://github.com/dydxopsdao/networks/blob/fd7ee6e63e7e4b3ffab4fe600ac7cdb77c28d88d/dydx-mainnet-1/genesis.json#L1135) at block height 6,912,000.

