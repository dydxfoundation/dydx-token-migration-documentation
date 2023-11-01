---
description: >-
  An overview of how to redelegate DYDX from one dYdX Chain validator to
  another.
---

# How to Redelegate Guide

## Overview

Redelegation in the Cosmos SDK is a feature that allows a delegator to shift 100% or a portion of their staked tokens (delegations) from one Validator to another without having to wait for the unbonding period.&#x20;

During the redelegation process, the tokens remain staked, meaning they continue to contribute to the network's security and potentially earn rewards for the delegator.

However, a user’s slashing risk with the original Validator remains until the unbonding period concludes. For example, a user stakes 20 DYDX to Validator A for 59 days, on day 60 the user decides to redelegate their 20 DYDX to Validator B. From days 60-90, the user is at a risk of having a portion of their 20 staked DYDX slashed based on the conduct of Validator A. After the 90th day, the slashing risk transitions to Validator B.

After redelegating, any DYDX that was redelegated must wait 30 days before it can be redelegated.

## Redelegate to another dYdX Chain validator

<figure><img src="../../.gitbook/assets/1(a) - Redelegate.png" alt=""><figcaption></figcaption></figure>

* 1(a) The [Keplr dashboard](https://wallet.keplr.app/chains/dydx) displays the Validators that you have staked to and the amount of tokens staked to each respective validator. Click on the arrow next to the Validator you’ve staked to previously.&#x20;

<figure><img src="../../.gitbook/assets/1(b) - Redelegate.png" alt=""><figcaption></figcaption></figure>

* 1(b) click “Redelegate”.

<figure><img src="../../.gitbook/assets/1(c) - Redelegate.png" alt=""><figcaption></figcaption></figure>

* 1(c) select the Validator that you would like to redelegate your DYDX tokens to and click “Next”.

<figure><img src="../../.gitbook/assets/1(d) - Redelegate.png" alt=""><figcaption></figcaption></figure>

* 1(d) enter the number of DYDX tokens that you want to redelegate, click ‘Redelegate’, and pay the gas fee on dYdX Chain.

<figure><img src="../../.gitbook/assets/1(e) - Redelegate.png" alt=""><figcaption></figcaption></figure>

* &#x20;1(e) Once the transaction to redelegate is complete, you will see your available balance updated on the dashboard.

\




\
