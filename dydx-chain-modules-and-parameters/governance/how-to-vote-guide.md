---
description: An overview of how to vote on a dYdX Chain governance proposal.
---

# How to Vote Guide

## Overview

Below, we provide a step-by-step guide to explain to new users of the dYdX Chain how to cast a vote on a governance proposal through Command Line Interface (CLI) or a wallet extension.

Note, only bonded DYDX tokens can vote on dYdX Chain governance proposals, and this guide was created with the assumption that you have bonded DYDX tokens.&#x20;

To get bonded DYDX tokens, you will need to stake your tokens to your preferred validator(s). Visit this [page](../staking/how-to-stake-guide.md) for further information on staking.

## Voting Method

* [Command Line Interface (CLI)](how-to-vote-guide.md#command-line-interface)
* [Keplr](how-to-vote-guide.md#keplr)
* [Leap](how-to-vote-guide.md#leap)

## Command Line Interface

1. To cast a vote, you must know the `proposalID` that they intend to vote on. You can query the list of proposals on dYdX Chain by entering this command on the CLI:

```
dydxprotocold query gov proposals
```

2. If you would like to know more details about the proposal, they can query it by entering this command on the CLI:

```sh
dydxprotocold query gov proposal <proposal-id>
```

3. Once you understand the subject matter being voted on and has formed an opinion about it, you can cast a vote by entering this command on the CLI:

```sh
dydxprotocold tx gov vote <proposal-id> <option> --from <key>
```

During the voting period, you may select a vote of either `Yes`, `No`, `Abstain`, or `NoWithVeto`.&#x20;

## Keplr

1. First, go to [Keplr Dashboard](https://wallet.keplr.app/). Once you can see the dashboard page, enter “dYdX” on the “Search Chains” bar on the upper left corner of the page.&#x20;

<figure><img src="../../.gitbook/assets/Image 09-11-23 at 20.41.jpeg" alt=""><figcaption></figcaption></figure>

2. Then click “dYdX” and you will be taken to dYdX dashboard.

<figure><img src="../../.gitbook/assets/Image 09-11-23 at 20.41 (1).jpeg" alt=""><figcaption></figcaption></figure>

3. Click the “Governance” tab, you will find all the information about current and past on-chain proposals.

<figure><img src="../../.gitbook/assets/Image 09-11-23 at 20.43.jpeg" alt=""><figcaption></figcaption></figure>

4. Proposals  that you can vote on are marked with the “Voting Period” tag.

<figure><img src="../../.gitbook/assets/Image 09-11-23 at 22.00.jpeg" alt=""><figcaption></figcaption></figure>

5. In case you have not had time to check out the [dYdX community forum](https://dydx.forum), you can read the full details of the proposal by clicking on the respective proposal.

<figure><img src="../../.gitbook/assets/Image 09-11-23 at 22.01.jpeg" alt=""><figcaption></figcaption></figure>

6. In the proposal page, you can find the Title, Proposal Timeline, Vote Details, Validator’s Review and Proposal Details.&#x20;

<figure><img src="../../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

7. Once you read the full description of the proposal, you can cast your vote by clicking the “Vote” button on the right side of the page.

<figure><img src="../../.gitbook/assets/Image 10-11-23 at 13.04.jpeg" alt=""><figcaption></figcaption></figure>

8. A pop-up of vote options will appear: `Yes`, `No`, `Abstain`, and `No With Veto`. To understand the difference between these options, you can visit the [Governance Module ](./#proposal-voting-options)documentation.&#x20;

<figure><img src="../../.gitbook/assets/Image 09-11-23 at 22.02.jpeg" alt=""><figcaption></figcaption></figure>

8. Once you have selected your preferred option, you can click "Confirm".

<figure><img src="../../.gitbook/assets/Image 09-11-23 at 22.02 (1).jpeg" alt=""><figcaption></figcaption></figure>

8. Keplr will prompt you to confirm the transaction, as well as show the transaction fee to cast the vote. After reviewing your selection and transaction fee, you can click "Approve".

<figure><img src="../../.gitbook/assets/Image 09-11-23 at 22.03.jpeg" alt=""><figcaption></figcaption></figure>

## Leap

1. First, go to [Leapboard](https://cosmos.leapwallet.io/): once on the Overview page, navigate to “Governance” on the left side of the page.

<figure><img src="https://lh7-eu.googleusercontent.com/W-IxQt1nDfHoo6jV8RYMXL2v-j8iFQkgN19RS2tz1GWveKlWZKdYJxo2E8ZDVQjklWeqwFJv-L6WyCyLe_uzQ-Lio4D0qV_9E5UuJXL6QPs6JXKkoJkUSnEA3ZElebAblF30AFepMwz9E3y3EXg4gKA" alt=""><figcaption></figcaption></figure>

2. On the Governance page, you can view the list of proposals that you can vote on. You can also click the “All Chains” drop-down menu on the upper right corner of the page to specifically find dYdX’s proposals.&#x20;

<figure><img src="https://lh7-eu.googleusercontent.com/VI_a8flqoJinxfgiYJF_a0zYBZlTqZnhKir_wXQtFXvaaUrKTb1rai-XitcuKm6WAZ1IBPveYzxtOIJi98ETWc-prIzHvOTyecQ3APtCJeG-R3NRh0b2ubj2IyG-urMLb57qp_jvqgBhGu4cOdWy0C4" alt=""><figcaption></figcaption></figure>

3. Click on the proposal that you want to vote on.&#x20;

<figure><img src="https://lh7-eu.googleusercontent.com/sFT-9OvRcV0uxtsaFZxDGJVytS0uTNfO5pGE1DopkwuvcMvVjWJ8Fj8L07tkhwRIGzQPLBBSys5hf-3FXidVgjIiEzc40hunyJ1ODRY-WQmQCVi2733HCz99_GOUJoETvaRmuRZ_mLz9JTHT_7q1GcU" alt=""><figcaption></figcaption></figure>

4. The proposal page will show the Vote Details, ChatGPT Summary (if available), Vote Timeline, Proposal Details, and Detailed Description.

<figure><img src="https://lh7-eu.googleusercontent.com/YgUSahSjmiuwxSBBhCj0I0HP36KH--F_CnVZQZqf3h6p9lC4ZfExcsmYr5MyDOi6IRBFz7THMwSikrM7Tiv3IHT6nUNhITC0SlCQpFyAdEqyLIX4dSgWftd-9VMrWibIYizg8C_GzGOHOupVowtNj3U" alt=""><figcaption></figcaption></figure>

5. In case you haven’t had time to check out the [dYdX community forum](https://dydx.forum), you can read the full details of the proposal by clicking the “Detailed Description”.

<figure><img src="https://lh7-eu.googleusercontent.com/3-xG7cvYEZ8cO-pcu-003VDoCodzSivy6d1B-7Trq3ktuMlMxkyDm_9kXmIbktszRoRHUmcJ_I0MF7nImkuUAUpm5kDa-kLYFUgX9IL39tZqBGbNNz59Z_uzsiqe335VwPtUvEl3_1G8_pxmu-ilAKk" alt=""><figcaption></figcaption></figure>

6. Once you read the full description of the proposal, you can cast your vote by clicking the “Vote” button on the upper right side of the page.&#x20;

<figure><img src="https://lh7-eu.googleusercontent.com/5HH3-Br8_eBX5BLusSnnubq0RrCvRDoS0_m3AiyBEJzH0n5Qsb540mKZNKW511nseCX3_9f2FhuKi1UG5lSauSH0gxznyNucdsplP4I2ZxdpTxoeuJTnap6BIT6wf35KgXfWqhUH1-qQ3LDdTlxfqwI" alt=""><figcaption></figcaption></figure>

7. A pop-up of vote options will appear: ‘Yes’, ‘No’, ‘Abstain’, and ‘No With Veto’.&#x20;

<figure><img src="https://lh7-eu.googleusercontent.com/I59NJHjLVCBp2587HoJUqThSTzF-sgIbqJb6Sc63VK_WrUQ28XJSbhm7-uI1143FXz1rR6ajOmwdJmx7CUo5ZIP0U4vlOZmpwO7xkC37bhqgOXiHgiXIP14_DSHspuFjyG1kHxpCleJ9JqnebyDaKI0" alt=""><figcaption></figcaption></figure>

8. Once you have selected your preferred option, you can click “Submit”.

<figure><img src="https://lh7-eu.googleusercontent.com/NRBWaJ-qGZy__rgaus0t54iJ6AMmo98-UN0Bn2DlnUIR1Nw_h8E5c5yIXrGMzb2K2eCBr4wns3iM-KCUR0_mBSDRVoTzi6gKIlZwzVxTCe0OUjiTD1W5rPdyHRCjy1Pdv9lCWxV3AYc5SE6XFGi5qWI" alt=""><figcaption></figcaption></figure>

9. Leap will prompt you to confirm the transaction, as well as showing the transaction fee to cast the vote. Once done, you can click “Approve”.

<figure><img src="https://lh7-eu.googleusercontent.com/hullkc7Bnf745O7hrXnxzad5WAhFOlGUBOVZdA_QIfej6qyjf6abDwFAoHeO7e6Bg949c3Y9YB7UMWqFNXeO2_dwpJ3XqtTFCXCVLfQHFOVr7DLFWVnNwMENRfRtfkjYWCwjrW6h9CJL41_fRfwXuRw" alt=""><figcaption></figcaption></figure>

\
\
