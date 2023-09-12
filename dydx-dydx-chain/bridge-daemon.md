---
description: An overview of the Bridge Daemon
---

# Bridge Daemon

### High-level Overview&#x20;

The [`Bridge Daemon`](https://github.com/dydxprotocol/v4-chain/tree/main/protocol/daemons/bridge) is implemented in the same way as other daemons in the dYdX Chain open source software. Specifically, the daemon:

* will be run in process as go routines, and
* will use gRPC for communication with the main application.&#x20;

### One-time Setup

1. Application initializes gRPC server
2. The daemon initializes gRPC client&#x20;
   1. need to make a connection to `localhost:9090` for query service
   2. need to make a connection to unix socket for private daemon service

## Related Module

[x-bridge-module.md](x-bridge-module.md "mention")



## Daemon

### Main Loop Logic

#### Query Protocol for the Next Event ID

Let `n` be the `nextRecognizedEventId` on the in-memory `BridgeEvents` struct on the`x/bridge` module.

Let `c` be the `ProposeParams.MaxBridgesPerBlock` parameter on the `x/bridge` module.

#### Search for next bridge log

For each Ethereum node endpoint configured, use the `eth_getLogs` RPC call with the following parameters:

* `address` : `BridgeContractAddress`
* `topics` : \[ `sha256(LogBridge(…))` , \[ `n` , `n+1` , … , `n+c-1` ]]
* `from_block` : `"ethereum block height of last recognized bridge event"`
* `to_block` : `"finalized"`

#### Update the Server

For each event returned by each of the Ethereum nodes, send a single, batched `AddBridgeEventsRequest` to the server with the events in-order.

#### Sleep

To prevent hogging resources (from the validator itself or the remote Ethereum Node), the go routine can sleep until the next iteration. It can use the `ProposeParams.ProposeDelayDuration` parameter on the `x/bridge` module to determine a suitable sleep time. Ideally it would sleep for no more than about half of this interval.

## Configuration

These should be configurable by a validator.&#x20;

`EthereumNodeRpcEndpoint` : The daemon maintains an Ethereum node RPC endpoint.

> Ideally, this should be a list of RPC endpoints and every RPC query will be sent to each node and daemon will only proceed if each node provides the same response. However, if a validator hosts its own Ethereum node, then it can use a single endpoint. All 16 private-testnet validators who responded to a dYdX survey indicated that they will host their own Ethereum full nodes.

`BridgeContractAddress` : The bridge contract to query logs from.



## RPC Interface

```
// BridgeService defines the gRPC service used by bridge daemon.
service BridgeService {
    // Sends a list of newly recognized bridge events.
    rpc AddBridgeEvents(AddBridgeEventsRequest)
        returns (AddBridgeEventsResponse);
}

// AddBridgeEventsRequest is a request message that contains a list of new bridge
// events. The events should be contiguous and sorted by (unique) id.
message AddBridgeEventsRequest {
    repeated dydxprotocol.bridge.BridgeEvent bridge_events = 1
        [ (gogoproto.nullable) = false ];
}

// AddBridgeEventsResponse is a response message for BridgeEventRequest.
message AddBridgeEventsResponse {}
```

Information is stored in the `BridgeEvent` struct as described in [x/bridge](x-bridge-module.md).
