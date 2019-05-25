# lptOrderBookApp

## Introduction and Objective

This document describes the use cases of an application installed in an Aragon DAO, to facilitate the exchange of bonded LPT for DAI. For bonded LPT to be withdrawn from its bonded state, an unbonding period must elapse (currently 7 rounds = ~6.5 days).

The objective of this app is to provide a guarantee that:

IF _a buyer and the DAO have agreed to an exchange_
AND _the buyer has committed funds to the purchase_
THEN _there is no way to stop it_, **except by stopping Ethereum from processing transactions.**

This avoids the requirement for the DAO (seller) to provide collateral as security for the buyer (to insure against the case that the agreed exchange does not complete as originally agreed.)

In order to use this application, LPT must first be deposited to the application, and bonded to a node in the network. (See Question 2 below).

## Scenario

A DAO has the lptOrderBookApp app installed, which has previously bonded LPT to a Transcoder in Livepeer's network.

Alice has the permission to create votes to create sell orders on the lptOrderBookApp app.

Bob has DAI and would like to purchase LPT. Bob doesn't mind waiting for the unbonding period to elapse before receiving LPT.

### DAO Initiates Exchange

This section describes the set of use cases for the app to allow the DAO which controls the bonded LPT to initiate an exchange, which a buyer can commit to.

#### Use Case 1 - FAILURE

- Alice creates a vote for the DAO to create a sell order of `X` LPT for `Y` DAI

- DAO votes No. End of story.

#### Use Case 2 - FAILURE

- Alice creates a vote for the DAO to create a sell order of `X` LPT for `Y` DAI

- DAO votes Yes to create order.

- Alice creates a vote to cancel sell order.

- DAO votes Yes and the order is cancelled. End of story.

#### Use Case 3 - SUCCESS

- Alice creates a vote for the DAO to create a sell order of `X` LPT for `Y` DAI

- DAO votes Yes to create order.

- Bob commits to buy, and deposits `Y` DAI. The app automatically unbonds `X` LPT. (See Question 1 below).

- The unbonding period elapses.

- Any entity instructs the app to withdraw `X` LPT and transfer to Alice.

### Buyer Initiates Exchange

This section describes the set of use cases for the app to allow a buyer of LPT to initiate an exchange which a DAO can commit to.

#### Use Case 4 - FAILURE

- Bob proposes a vote for the DAO to sell them `X` bonded LPT to for `Y` DAI, and deposits `Y` DAI

- Bob withdraws `Y` DAI (Question 3, see below)

#### Use Case 5 - FAILURE

- Bob proposes a vote for the DAO to sell them `X` bonded LPT to for `Y` DAI, and deposits `Y` DAI

- The DAO votes No, and the `Y` DAI are released back to Bob.

#### Use Case 6 - SUCCESS

- Bob proposes a vote for the DAO to sell them `X` bonded LPT to for `Y` DAI, and deposits `Y` DAI

- The DAO votes Yes, which commits it to sell. The app automatically unbonds `X` LPT. (See Question 1 below).

- The unbonding period elapses.

- Any entity permissionlessly instructs the app to withdraw and transfer `X` LPT to Bob.

## Questions

Question 1: Is it actually possible to guarantee that this exchange will happen? Some potential attack vectors:

- The DAO updates the application to make previously permissionless functions permissioned and controlled by the DAO.
- The DAO updates permissions to allow the DAO to withdraw and transfer
- Livepeer pauses its protocol indefinitely.
- Aragon makes an update to their OS allowing something unforeseen? Like what?

Question 2: Is there a way to make it so that a DAO can unbond, withdraw and transfer via the lptOrderBookApp app, independently of this process above, or would that require permissions to be given to a function which would compromise these processes?

Question 3: if Bob proposes a vote for the DAO to sell what could happen to the vote? Could this cancel it? Or would it just be made unpassable?)
