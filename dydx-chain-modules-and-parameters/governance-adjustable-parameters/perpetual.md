# Perpetual

## Funding Rate

Perpetual contracts, unlike traditional futures contracts, lack an expiry date and use funding rates to encourage the perpetual price to align with the underlying asset's price. The Funding Rate is determined algorithmically based on the Index Price and Mid-Market Prices, prompts long traders to pay shorts when the perpetual trades at a premium and vice versa.&#x20;

These payments are proportional to traders' positions and are exchanged directly between traders, not involving the exchange. The goal of the Funding Rate is to maintain the perpetual market's price close to the Index Price by incentivizing trading actions that bring it in line with the underlying asset's value.

<table data-header-hidden><thead><tr><th width="341"></th><th width="173"></th><th width="331"></th></tr></thead><tbody><tr><td>Title</td><td>Value</td><td>Definition</td></tr><tr><td><a href="https://github.com/dydxopsdao/networks/blob/fd7ee6e63e7e4b3ffab4fe600ac7cdb77c28d88d/dydx-mainnet-1/genesis.json#L3288"><code>funding_rate_clamp_factor_ppm</code></a></td><td>6000000 [6%]</td><td>Used for clamping 8-hour Funding Rates according to the equation: <code>funding_rate_clamp_factor * (initial margin - maintenance margin)</code>.</td></tr><tr><td><a href="https://github.com/dydxopsdao/networks/blob/fd7ee6e63e7e4b3ffab4fe600ac7cdb77c28d88d/dydx-mainnet-1/genesis.json#L3289"><code>premium_vote_clamp_factor_ppm</code></a></td><td>60000000 [60%]</td><td>Used for clamping 8-hour Premium Votes according to the equation: <code>premium_vote_clamp_factor * (initial margin - maintenance margin)</code>.</td></tr><tr><td><a href="https://github.com/dydxopsdao/networks/blob/fd7ee6e63e7e4b3ffab4fe600ac7cdb77c28d88d/dydx-mainnet-1/genesis.json#L3290"><code>min_num_votes_per_sample</code></a></td><td>15</td><td>Minimum number of premium votes per premium sample.</td></tr></tbody></table>

## Epoch Information

Funding rate and premium payments are credited or debited at a fixed interval based on the Epoch Information parameters. These parameters define the funding rate interval and premium sampling interval:

* Next Tick: when the next epoch starts in seconds.
* Duration: duration of the epoch in seconds.
* Is Initialized: whether the epoch has been initialized.&#x20;
* Fast Forward Next Tick: specifies whether `next_tick`.
* should be fast-forwarded to be greater than the current block time.

<table data-header-hidden><thead><tr><th width="275"></th><th></th><th width="108"></th><th></th><th></th><th width="107"></th><th></th></tr></thead><tbody><tr><td>Name</td><td><p>Next Tick</p><p><br></p></td><td><p>Duration</p><p>(seconds)</p></td><td>Current Epoch</td><td>Current Epoch Start Block</td><td>Is Initialized </td><td>Fast Forward Next Tick </td></tr><tr><td><a href="https://github.com/dydxopsdao/networks/blob/fd7ee6e63e7e4b3ffab4fe600ac7cdb77c28d88d/dydx-mainnet-1/genesis.json#L1162-L1168"><code>funding-sample</code></a></td><td>30</td><td>60</td><td>0</td><td>0</td><td>False</td><td>True</td></tr><tr><td><a href="https://github.com/dydxopsdao/networks/blob/fd7ee6e63e7e4b3ffab4fe600ac7cdb77c28d88d/dydx-mainnet-1/genesis.json#L1171-L1177"><code>funding-tick</code></a></td><td>0</td><td>3600</td><td>0</td><td>0</td><td>False</td><td>True</td></tr><tr><td><a href="https://github.com/dydxopsdao/networks/blob/fd7ee6e63e7e4b3ffab4fe600ac7cdb77c28d88d/dydx-mainnet-1/genesis.json#L1180-L1186"><code>stats-epoch</code></a></td><td>0</td><td>3600</td><td>0</td><td>0</td><td>False</td><td>True</td></tr></tbody></table>

