# Safety

## Spam Mitigation

The following strategies that can be updated by governance exist to prevent spam on the orderbook and prevent the blockchain state from getting too large:

### Block Rate Limit

Block rate limit defines the block rate limits for CLOB specific operations.

<table data-header-hidden><thead><tr><th width="449"></th><th width="129"></th><th width="145"></th><th width="180"></th></tr></thead><tbody><tr><td>Title</td><td>Limit</td><td>Num_blocks</td><td>Definition</td></tr><tr><td><a href="https://github.com/dydxopsdao/networks/blob/fd7ee6e63e7e4b3ffab4fe600ac7cdb77c28d88d/dydx-mainnet-1/genesis.json#L966-L971">max_short_term_orders_per_n_blocks</a></td><td>200</td><td>1</td><td>How many short term order attempts (successful and failed) are allowed for an account per N blocks. </td></tr><tr><td><a href="https://github.com/dydxopsdao/networks/blob/fd7ee6e63e7e4b3ffab4fe600ac7cdb77c28d88d/dydx-mainnet-1/genesis.json#L972-L981">max_stateful_orders_per_n_blocks</a></td><td><p>2</p><p>20</p></td><td><p>1</p><p>100</p></td><td>How many stateful order attempts (successful and failed) are allowed for an account per N blocks. </td></tr><tr><td><a href="https://github.com/dydxopsdao/networks/blob/fd7ee6e63e7e4b3ffab4fe600ac7cdb77c28d88d/dydx-mainnet-1/genesis.json#L982-L987">max_short_term_order_cancellations_per_n_blocks</a></td><td>200</td><td>1</td><td>How many short term order cancellation attempts (successful and failed) are allowed for an account per N blocks. </td></tr></tbody></table>

## Equity Tier Limit

Equity tier limit defines the set of equity tiers to limit how many open orders a subaccount is allowed to have.

<table data-header-hidden><thead><tr><th width="313"></th><th></th><th width="167"></th><th width="239"></th></tr></thead><tbody><tr><td>Title</td><td>limit</td><td>usd_tnc_required</td><td>Definition</td></tr><tr><td><a href="https://github.com/dydxopsdao/networks/blob/fd7ee6e63e7e4b3ffab4fe600ac7cdb77c28d88d/dydx-mainnet-1/genesis.json#L990-L1015">short_term_order_equity_tiers</a></td><td>0</td><td>0</td><td><p>how many open short term orders are allowed per equity tier.</p><p><br></p></td></tr><tr><td></td><td>4</td><td>20000000</td><td></td></tr><tr><td></td><td>8</td><td>100000000</td><td></td></tr><tr><td></td><td>10</td><td>1000000000</td><td></td></tr><tr><td></td><td>100</td><td>10000000000</td><td></td></tr><tr><td></td><td>1000</td><td>100000000000</td><td></td></tr><tr><td><a href="https://github.com/dydxopsdao/networks/blob/fd7ee6e63e7e4b3ffab4fe600ac7cdb77c28d88d/dydx-mainnet-1/genesis.json#L1016-L1041">stateful_order_equity_tiers</a></td><td>0</td><td>0</td><td>how many open stateful orders are allowed per equity tier.</td></tr><tr><td></td><td>4</td><td>20000000</td><td></td></tr><tr><td></td><td>8</td><td>100000000</td><td></td></tr><tr><td></td><td>10</td><td>1000000000</td><td></td></tr><tr><td></td><td>100</td><td>10000000000</td><td></td></tr><tr><td></td><td>200</td><td>100000000000</td><td></td></tr></tbody></table>

\
