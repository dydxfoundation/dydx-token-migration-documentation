# Trading Core

## Insurance Fund

The insurance fund (\`dydx1c7ptc87hkd54e3r7zjy92q29xkq7t79w64slrq\`) is the first backstop to maintain the solvency of the system when an account has a negative balance. The account will be liquidated, and the insurance fund will take on the loss when it occurs. This insurance fund will be used before any deleveraging occurs.

The current size of the insurance fund can be viewed [here](https://www.mintscan.io/dydx/address/dydx1c7ptc87hkd54e3r7zjy92q29xkq7t79w64slrq).&#x20;

### Deleveraging

If the insurance fund is depleted, positions with the highest profit and leverage may be used to offset negative-balance accounts, ensuring system stability. This process, known as **deleveraging**, is a last-resort feature in perpetual contracts.&#x20;

It works similarly to "auto-deleveraging" in other markets, requiring profitable traders to contribute profits to offset underwater accounts. Deleveraging is used only when the insurance fund is depleted and prioritizes high-profit, high-leverage accounts. This approach reduces uncertainty for traders at lower risk levels compared to a socialized loss mechanism. The most highly leveraged offsetting accounts are deleveraged first.

{% hint style="info" %}
#### _Deleveraging Example_

Assume an initial margin requirement of 10% and a maintenance margin requirement of 7.5%.

Trader A deposits 1000 USDC, then opens a long position of 1 BTC at a price of 2000 USDC. Their account balance is -1000 USDC, +1 BTC. During a period of intense and prolonged volatility, the index price reaches 1080 USDC. Trader A is in a risky position, but not yet liquidatable. The price then rapidly drops further, and before A can be liquidated, the index price reaches 900 USDC, making the nominal value of A’s account -100 USDC.

The insurance fund is already depleted due to recent price swings, so deleveraging kicks in. Trader B, whose current balance is 10000 USDC, -9 BTC, is selected as the counterparty, on the basis of B’s profit and leverage, and the fact that B’s short position can offset A’s long position.

Trader B receives A’s entire balance, leaving A with zero balance, and bringing B’s total balance to 9000 USDC, -8 BTC. Trader B’s nominal loss due to deleveraging is 100 USDC, at an index price of 900 USDC. Trader B’s margin percentage increased (and leverage decreased) as a result of deleveraging, from 23.46% to 25%.
{% endhint %}

## Liquidations Config

When accounts fall below the maintenance margin requirement, the liquidation engine can automatically close their positions at the specified liquidation price. The insurance fund absorbs any profits or losses resulting from these liquidations.&#x20;

<table data-header-hidden><thead><tr><th width="440"></th><th width="170"></th><th width="261"></th></tr></thead><tbody><tr><td>Title</td><td>Value</td><td>Definition</td></tr><tr><td><a href="https://github.com/dydxopsdao/networks/blob/fd7ee6e63e7e4b3ffab4fe600ac7cdb77c28d88d/dydx-mainnet-1/genesis.json#L951"><code>max_liquidation_fee_ppm</code></a></td><td>15000 [0.015%]</td><td>When an account is liquidated, up to the entire value of the account may be taken as penalty and transferred to the Insurance Fund. The liquidation engine will attempt to leave funds in accounts of positive value where possible after they have paid the maximum liquidation fee.</td></tr><tr><td><a href="https://github.com/dydxopsdao/networks/blob/fd7ee6e63e7e4b3ffab4fe600ac7cdb77c28d88d/dydx-mainnet-1/genesis.json#L952-L955"><code>position_block_limits</code></a></td><td>Contains the following parameter values:</td><td>The minimum (in notional value) and maximum (in parts per million) amount of how much a single position can be liquidated within one block.</td></tr><tr><td><a href="https://github.com/dydxopsdao/networks/blob/fd7ee6e63e7e4b3ffab4fe600ac7cdb77c28d88d/dydx-mainnet-1/genesis.json#L953"><code>min_position_notional_liquidated</code></a></td><td>‎1000000000</td><td></td></tr><tr><td><a href="https://github.com/dydxopsdao/networks/blob/fd7ee6e63e7e4b3ffab4fe600ac7cdb77c28d88d/dydx-mainnet-1/genesis.json#L954"><code>max_position_portion_liquidated_ppm</code></a></td><td>100000 [0.1%]</td><td></td></tr><tr><td><a href="https://github.com/dydxopsdao/networks/blob/fd7ee6e63e7e4b3ffab4fe600ac7cdb77c28d88d/dydx-mainnet-1/genesis.json#L956-L959"><code>subaccount_block_limits</code></a></td><td>Contains the following parameter values:</td><td>The maximum amount of how much a single subaccount can be liquidated within a single block in notional value.</td></tr><tr><td><a href="https://github.com/dydxopsdao/networks/blob/fd7ee6e63e7e4b3ffab4fe600ac7cdb77c28d88d/dydx-mainnet-1/genesis.json#L957"><code>max_notional_liquidated</code></a></td><td>100000000000</td><td></td></tr><tr><td><a href="https://github.com/dydxopsdao/networks/blob/fd7ee6e63e7e4b3ffab4fe600ac7cdb77c28d88d/dydx-mainnet-1/genesis.json#L958"><code>max_quantums_insurance_lost</code></a></td><td><p>1000000000000</p><p><br></p></td><td>The maximum number of quote quantums (exclusive) that the Insurance Fund can have for deleverages to be enabled.</td></tr><tr><td><a href="https://github.com/dydxopsdao/networks/blob/fd7ee6e63e7e4b3ffab4fe600ac7cdb77c28d88d/dydx-mainnet-1/genesis.json#L960-L963"><code>fillable_price_config</code></a></td><td>Contains the following parameter values:</td><td>Configuration regarding how the fillable-price spread from the oracle price increases based on the adjusted bankruptcy rating of the subaccount.</td></tr><tr><td><a href="https://github.com/dydxopsdao/networks/blob/fd7ee6e63e7e4b3ffab4fe600ac7cdb77c28d88d/dydx-mainnet-1/genesis.json#L961"><code>bankruptcy_adjustment_ppm</code></a></td><td>1000000 [1%]</td><td></td></tr><tr><td><a href="https://github.com/dydxopsdao/networks/blob/fd7ee6e63e7e4b3ffab4fe600ac7cdb77c28d88d/dydx-mainnet-1/genesis.json#L962"><code>spread_to_maintenance_margin_ratio_ppm</code></a></td><td>1500000 [1.5%]</td><td></td></tr></tbody></table>
