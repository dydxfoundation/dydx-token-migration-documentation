---
description: An overview of the x/bridge module
---

# 🌉 x/bridge module

The [`x/bridge module`](https://github.com/dydxprotocol/v4-chain/tree/main/protocol/x/bridge) ([`dydx1zlefkpe3g0vvm9a4h0jf9000lmqutlh9jwjnsv`](https://www.mintscan.io/dydx/address/dydx1zlefkpe3g0vvm9a4h0jf9000lmqutlh9jwjnsv)) is responsible for receiving bridged tokens from the Ethereum blockchain. It has an associated [`daemon`](https://github.com/dydxprotocol/v4-chain/tree/main/protocol/daemons/bridge) that knows about all “bridge events” that happened on Ethereum by making RPC calls to an Ethereum full node. Bridge events are logs emitted by the bridging smart-contract on Ethereum. Each event has a unique, sequentially-increasing `id`.

## Concepts&#x20;

### [Event States](https://github.com/dydxprotocol/v4-chain/tree/main/protocol/x/bridge/types)&#x20;

A bridge event can be considered to be in one of the following states:&#x20;

<table><thead><tr><th width="198">State</th><th>Description</th></tr></thead><tbody><tr><td><code>EthMined</code></td><td>Included in the Ethereum blockchain</td></tr><tr><td><code>EthFinalized</code></td><td>Included in the Ethereum blockchain in a block that has been finalized</td></tr><tr><td><code>Recognized</code></td><td><ul><li>Understood to be finalized by an individual validator’s bridge daemon </li></ul><ul><li>Not in consensus </li></ul><ul><li>dYdX Chain validators should only propose <code>Recognized</code> events for inclusion in blocks after an additional waiting period (configured in the <code>ProposeParams)</code> in order to give enough time for other validators to recognize the event</li></ul></td></tr><tr><td><code>Acknowledged</code></td><td><ul><li>Included in a block on the open-source v4 chain developed by dYdX (”v4”) by a proposer and validated with +2⁄3 weight </li></ul><ul><li>In consensus</li></ul></td></tr><tr><td><code>Completed</code></td><td><ul><li>Was <code>Acknowledged</code> for a certain number of blocks</li><li>Has resulted in newly-minted tokens on v4 </li><li>In consensus </li><li>The block-delay (configured in the <code>SafetyParams</code>) gives the validators the chance to halt or hard-fork the chain in the disaster-case of accidentally recognizing an invalid event</li></ul></td></tr></tbody></table>



## Messages

### Injectable Transactions&#x20;

`MsgAcknowledgeBridges`

This message is injected by the block proposer.&#x20;

It should be rejected during `ProcessProposal` if any of below is true

* event IDs are not sequential
* first event’s `id` does not match `NextAcknowledgeEventId` in state.
* last event’s `id` is not recognized yet.
* any event’s content does not match what’s in state.

For each bridge event, it delays a MsgCompleteBridge (see below) using x/delaymsg module to be executed SafetyParams.delay\_blocks blocks later.

```
message MsgAcknowledgeBridges {
    repeated BridgeEvent event = 1;
}
```



`MsgCompleteBridge`&#x20;

This message should only be sent by the `x/delaymsg` module. It will mint tokens to the specified address by transferring from the bridge module account. The `id` does not have to be verified.

```
message CompleteBridge {
  option (cosmos.msg.v1.signer) = "authority";
  string authority = 1 [(cosmos_proto.scalar) = "cosmos.AddressString"];
  BridgeEvent event = 2;
}
```



### ABCI Messages

`PrepareProposal`

Let the wall-clock time of the proposer be wallClock. Let the block timestamp be blockTimestamp. In order to ensure an upper-bound on liveness issues in the case that +⅓ of validators cannot properly get logs from an Ethereum node, we will often skip proposing bridge events at all. Since we expect the rate of bridge events to be much lower than 1 per v4 block, we use a combination of probabilistic (based on pseudo-randomness) and deterministic (based on time) skipping. Therefore, skip this step altogether (by proposing a bridge tx with empty bridge events) if either of the following:

* `rand.Uint32(1_000_000) < ProposeParams.skip_rate_ppm`&#x20;
* `blockTimestamp ≤ wallClock - ProposeParams.skip_if_block_delayed_by_duration`

In `PrepareProposal`, the proposer will inject one `MsgAcknowledgeBridges` transaction that includes at most `ProposeParams.max_bridges_per_block` bridge events (in order of `id`), which need to satisfy following criteria

* An `id` greater-than-or-equal-to the `NextAcknowledgeEventId`
* A `recognizedAt ≤ wallClock - ProposeParams.propose_delay_duration`



### Governance Messages&#x20;

`MsgUpdateEventParams`

```
message MsgUpdateEventParams {
    string authority = 1;
    EventParams params = 2;
}
```



`MsgUpdateSafetyParams`

```
message MsgUpdateSafetyParams {
    string authority = 1;
    SafetyParams params = 2;
}
```



`MsgUpdateProposeParams`

```
message MsgUpdateProposeParams {
    string authority = 1;
    ProposeParams params = 2;
}
```



## Queries

```
service Query {
    rpc EventParams(QueryEventParamsRequest)
        returns (QueryEventParamsResponse);

    rpc SafetyParams(QuerySafetyParamsRequest)
        returns (QuerySafetyParamsResponse);

    rpc ProposeParams(QueryProposeParamsRequest)
        returns (QueryProposeParamsResponse);

    rpc NextAcknowledgedEventId(QueryNextAcknowledgedEventIdRequest)
        returns (QueryNextAcknowledgedEventIdResponse);
    rpc NextRecognizedEventId(QueryNextRecognizedEventIdRequest)
        returns (QueryNextRecognizedEventIdResponse);
}

message QueryEventParamsRequest {}
message QueryEventParamsResponse {
    EventParams params = 1;
}

message QuerySafetyParamsRequest {}
message QuerySafetyParamsResponse {
    SafetyParams params = 1;
}

message QueryProposeParamsRequest {}
message QueryProposeParamsResponse {
    ProposeParams params = 1;
}

message QueryNextAcknowledgedEventIdRequest {}
message QueryNextAcknowledgedEventIdResponse {
    uint32 id = 1;
}

message QueryNextRecognizedEventIdRequest {}
message QueryNextRecognizedEventIdResponse {
    uint32 id = 1;
}
```

***

## [Keeper Methods](https://github.com/dydxprotocol/v4-chain/tree/main/protocol/x/bridge/keeper)

### Bridging

**`GetRecognizedEventInfo`**

Returns the `RecognizedEventInfo` from the `BridgeEventManager`. This has the next event `id` that has not yet been recognized by this node’s daemon. This also has the height of the highest Ethereum block from which a bridge event was recognized. These values are not in-consensus.

```go
func (k Keeper) **GetRecognizedEventInfo**(
  ctx sdk.Context,
): BridgeEventInfo
```

**`GetAcknowledgedEventInfo`**

Returns the `AcknowledgedEventInfo` from state.

```go
func (k Keeper) **GetAcknowledgedEventInfo**(
  ctx sdk.Context,
): BridgeEventInfo
```

**`AcknowledgeBridges`**

For each bridge event, sends a message to the `x/delay-msg` module, wrapping a `MsgCompleteBridge` to be executed `SafetyParams.delay_blocks` blocks in the future. Update `AcknowledgedEventInfo` in state.

```go
func (k Keeper) AcknowledgeBridges(
  ctx sdk.Context,
	bridges []BridgeEvent,
): (
  err error,
)
```

**`CompleteBridge`**

Processes a bridge event by transfering the appropriate tokens to the given address from bridge module account. The `id` of the bridge is not validated as it should have already been validated by `AcknowledgeBridges`.

```go
func (k Keeper) CompleteBridge(
  ctx sdk.Context,
	bridge BridgeEvent,
): (
  err error,
)
```

### [Params](https://github.com/dydxprotocol/v4-chain/blob/main/protocol/x/bridge/keeper/params.go)

`GetEventParams`&#x20;

Returns the `EventParams` from state.

```
func (k Keeper) GetEventParams(
    ctx sdk.Context,
): (
    params EventParams,
)
```



`GetSafetyParams`&#x20;

Returns the `SafetyParams` from state.

```
func (k Keeper) GetSafetyParams(
    ctx sdk.Context,
): (
    params SafetyParams,
)
```



`GetProposeParams`&#x20;

Returns the `ProposeParams` from state.

```
func (k Keeper) GetProposeParams(
    ctx sdk.Context,
): (
    params ProposeParams,
)
```



`UpdateEventParams`

Overwrites the `EventParams` in state. Returns an error and does not update the params if they fail basic validation.

```
func (k Keeper) UpdateEventParams(
    ctx sdk.Context,
    params EventParams,
): (
    err error,
)
```



`UpdateSafetyParams`

Overwrites the SafetyParams in state. Returns an error and does not update the params if they fail basic validation.

```
func (k Keeper) UpdateSafetyParams(
    ctx sdk.Context,
    params SafetyParams,
): (
    err error,
)
```



`UpdateProposeParams`

Overwrites the ProposeParams in state. Returns an error and does not update the params if they fail basic validation.

```
func (k Keeper) UpdateProposeParams(
    ctx sdk.Context,
    params ProposeParams,
): (
    err error,
)
```



***



## Store Data-Structures

### Bridge Store&#x20;

**`AcknowledgedEventInfo`**

`BridgeEventInfo`

Stores information about the next event `id` to acknowledge (`next_id`). The bridge daemon should query for this event `id` next.

Also stores the Ethereum block height of the most recently acknowledged event. Ethereum block heights strictly lower than this number do not have to be checked by the daemon.

In practice, these value should be set to positive numbers at genesis since some of the bridging events should be included in genesis state.

```protobuf
message BridgeEventInfo {
	// The next event id (the last processed id plus one) of the logs from the
	// Ethereum contract.
	uint32 next_id = 1;

	// The Ethereum block height of the most recently acknowledged bridge event.
	uint64 eth_block_height = 2;
}
```

### Param Store&#x20;

**`EventParams`**

`EventParams`

Stores parameters about which events to recognize and which tokens to mint. Used by the daemon to sanity-check information. Is not used directly by the module logic.

```
message EventParams {
    // The denom of the token to mint.
    string denom = 1;

    // The numerical chain ID of the Ethereum chain to query.
    uint64 eth_chain_id = 2;

    // The address of the Ethereum contract to monitor for logs.
    string eth_address = 3;
}
```



**`ProposeParams`**

`ProposeParams`

Holds the proposal parameters for the module.

```
message ProposeParams {
    // The maximum number of bridge events to propose per block.
    // Limits the number of events to propose in a single block
    // in-order to smooth out the flow of events.
    uint32 max_bridges_per_block = 1;
  
    // The minimum amount of nanoseconds to wait between a finalized bridge and
    // proposing it. This allows other validators to have enough time to
    // also recognize its occurence. Therefore the bridge daemon should
    // poll for new finalized events at least as often as this parameter.
    google.protobuf.Duration propose_delay_duration = 2;
    
    // Do not propose any events if a random number generator
    // (between 0 and 1_000_000) generates a number smaller than this number.
    uint32 skip_rate_ppm = 3;
    
    // Do not propose any events if the timestamp of the proposal block is
    // behind the proposers' wall-clock by at least this duration.
    google.protobuf.Duration skip_if_block_delayed_by_duration = 4;
}
```



**`SafetyParams`**

`SafetyParams`

Holds the safety parameters for the module.

```
message SafetyParams {
    // True if bridging is disabled.
    bool is_disabled = 1;

    // The number of blocks that bridges accepted in-consensus will be pending
    // until the minted tokens are granted.
    uint32 delay_blocks = 2;
}
```



## In-Memory Data-Structures

The keeper stores the bridge events in a go-routine safe map which is keyed by `id`.

```
// BridgeEventManager maintains a map of "Recognized" Bridge Events.
// That is, events that have been finalized on Ethereum but are
// not yet in consensus on the dYdX Chain. Methods are goroutine safe.
type BridgeEventManager struct {
    // Exclusive mutex taken when reading or writing
    sync.Mutex
    // Bridge events by ID
    events map[uint32]types.BridgeEventWithTime
    // Next unused key in the bridges map
    nextRecognizedEventId uint32
    // Time provider than can mocked out if necessary
    timeProvider lib.TimeProvider
}

// BridgeEventWithTime is a type that wraps BridgeEvent but also
// holds an additional timestamp.
type BridgeEventWithTime struct {
    event types.BridgeEvent
    timestamp time.Time
}
```

***

## Types

### Protos

```
message BridgeEvent {
    // The unique id of the Ethereum event log.
    uint32 id = 1;

    // The tokens bridged.
    cosmos.base.v1beta1.Coin coin = 2
        [ (gogoproto.nullable) = false ];

    // The account address or module address to bridge to.
    string address = 3
        [ (cosmos_proto.scalar) = "cosmos.AddressString" ];
}
```



