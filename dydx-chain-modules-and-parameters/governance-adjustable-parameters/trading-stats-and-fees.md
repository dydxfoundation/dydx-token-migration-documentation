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

<table data-header-hidden><thead><tr><th width="88"></th><th width="159"></th><th width="143"></th><th width="144"></th><th width="93"></th><th></th></tr></thead><tbody><tr><td>Tier</td><td><p>Absolute_volume_requirement</p><p>[30 day Trailing Volume]</p></td><td><p>Total_volume_share_requirement_ppm</p><p>[Exchange Market Share]</p></td><td><p>Maker_volume_share_requirement_ppm</p><p>[Maker Market Share]</p></td><td><p>maker_fee_ppm</p><p>[Maker Fee (bps)]</p></td><td><p>Taker_fee_ppm</p><p>[Taker Fee (bps)]</p></td></tr><tr><td><a href="https://github.com/dydxopsdao/networks/blob/fd7ee6e63e7e4b3ffab4fe600ac7cdb77c28d88d/dydx-mainnet-1/genesis.json#L1061-L1066">1</a></td><td>0 [&#x3C; $1M]</td><td>0 [-]</td><td>0 [-]</td><td>100 [1.0]</td><td>500 [5.0]</td></tr><tr><td><a href="https://github.com/dydxopsdao/networks/blob/fd7ee6e63e7e4b3ffab4fe600ac7cdb77c28d88d/dydx-mainnet-1/genesis.json#L1069-L1074">2</a></td><td>1000000000000 [≥ $1M]</td><td>0 [-]</td><td>0 [-]</td><td>100 [1.0]</td><td>450 [4.5]</td></tr><tr><td><a href="https://github.com/dydxopsdao/networks/blob/fd7ee6e63e7e4b3ffab4fe600ac7cdb77c28d88d/dydx-mainnet-1/genesis.json#L1077-L1082">3</a></td><td>5000000000000 [≥ $5M]</td><td>0 [-]</td><td>0 [-]</td><td>50 [0.5]</td><td>400 [4.0]</td></tr><tr><td><a href="https://github.com/dydxopsdao/networks/blob/fd7ee6e63e7e4b3ffab4fe600ac7cdb77c28d88d/dydx-mainnet-1/genesis.json#L1085-L1090">4</a></td><td>25000000000000 [≥ $25M]</td><td>0 [-]</td><td>0 [-]</td><td>0 [-]</td><td>350 [3.5]</td></tr><tr><td><a href="https://github.com/dydxopsdao/networks/blob/fd7ee6e63e7e4b3ffab4fe600ac7cdb77c28d88d/dydx-mainnet-1/genesis.json#L1093-L1098">5</a></td><td>125000000000000 [≥ $125M]</td><td>0 [-]</td><td>0 [-]</td><td>0 [-]</td><td>300 [3.0]</td></tr><tr><td><a href="https://github.com/dydxopsdao/networks/blob/fd7ee6e63e7e4b3ffab4fe600ac7cdb77c28d88d/dydx-mainnet-1/genesis.json#L1101-L1106">6</a></td><td>125000000000000 [≥ $125M]</td><td>5000 [≥ 0.5%]</td><td>0 [-]</td><td>-50 [-0.5]</td><td>250 [2.5]</td></tr><tr><td><a href="https://github.com/dydxopsdao/networks/blob/fd7ee6e63e7e4b3ffab4fe600ac7cdb77c28d88d/dydx-mainnet-1/genesis.json#L1109-L1114">7</a></td><td>125000000000000 [≥ $125M]</td><td>5000 [≥ 0.5%]</td><td>10000 [≥ 1%]</td><td>-70 [-0.7]</td><td>250 [2.5]</td></tr><tr><td><a href="https://github.com/dydxopsdao/networks/blob/fd7ee6e63e7e4b3ffab4fe600ac7cdb77c28d88d/dydx-mainnet-1/genesis.json#L1117-L1122">8</a></td><td>125000000000000 [≥ $125M]</td><td>5000 [≥ 0.5%]</td><td>20000 [≥ 2%]</td><td>-90 [-0.9]</td><td>250 [2.5]</td></tr><tr><td><a href="https://github.com/dydxopsdao/networks/blob/fd7ee6e63e7e4b3ffab4fe600ac7cdb77c28d88d/dydx-mainnet-1/genesis.json#L1125-L1130">9</a></td><td>125000000000000 [≥ $125M]</td><td>5000 [≥ 0.5%]</td><td>40000 [≥ 4%]</td><td>-110 [-1.1]</td><td>250 [2.5]</td></tr></tbody></table>

This fee tier was [implemented](https://github.com/dydxopsdao/networks/blob/fd7ee6e63e7e4b3ffab4fe600ac7cdb77c28d88d/dydx-mainnet-1/genesis.json#L1135) at block height 6,912,000.

