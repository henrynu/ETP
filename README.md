# The Creation Of NuLagoon Exchange-traded Pool A, and its sub-funds BearBTC and BullBTC

We are very proud to announce that we will create the first exchanged traded Nubits liquidity pool (Pool ET) in a few days.

For NuShareholders:
For Pool ET holders:
F


## Basic Key Features:

- The money from the sale of NuLagoon ETP A will be used in the liquidity operation to support Nubits trading at $1. As a compensation, NuShareholders grant NuLagoon custodian fee, 
which will be shared by liquidity Pool A, C, D and ETP A.

- Typically, about half of the holding in ETP A will be in the form of BTC. As a result, the NAV of ETP A will fluctuate along the price of BTC. For users who are familiar with NuLagoon,
 ETP A's NAV goes exact same way as Pool A.
 
- Using coin control feature to send 1000 (or more) NBT to any of ETP A sub-funds addresses to purchase ETP A shares.
 
- Using coin control feature to send some NBT from a specific user address to any of ETP A sub-funds addresses to redeem ETP A shares.

- ETP A will be open to purchase and redemption once a month. Before the trading volume on the exchange reaches a level to provide enough liquidity, ETP A is open every Monday.

## More Features

- The ETP A shares purchased will automatically spilt to shares BearBTC and BullBTC with same number of each.
 
- BearBTC and BullBTC share holders can transfer his/her shares to another person.

- BearBTC and BullBTC share holders can sell his/her shares for Nubits on the exchange

- Users can directly buy BearBTC and BullBTC shares from the exchange


# Part 1: Off Exchange Interface

## - Purchase

To submit a purchase order, user send 1000 (or more) NBT from a specified send-from address to BearBTC or BullBTC share address. Purchase order will be accepted at end of each month after 
the EOM NAV of pool shares is computed. The ET Pool shares purchased will automatically spilt into ET BearBTC and ET BullBTC with same number of shares of each instrument. The send-from address
will be registered as UserAddr in NuLagoon. The formula is as follow:

```
the number of ET BearBTC share purchased = purchase amount / ( NAV of ET BearBTC + NAV of ET BullBTC )
the number of ET BullBTC share purchased = purchase amount / ( NAV of ET BearBTC + NAV of ET BullBTC )
```

- Example of a Nubits transaction:

> input:
> - Bxxxxxxxxx , ...
> - Byyyyyyyyy , ...

> output:
> - BBearBTCaddr, 1000
> - Bzzzzzzzzzzz, ....
 
> Assuming the NAV of BearBTC is 1.1 and the NAV of BearBTC is 0.9, then 500 share of BearBTC and 500 share of BullBTC will be credit to UserAddr Bxxxxxxxxx.

## - Redemption

To submit a redemption order, user send a certain amount of NBT from UserAddr to NuLagoon purchase address. Redemption order will be accepted at end of each month after 
the EOM NAV of pool shares is computed. Redemption requires the same number of BearBTC share and BullBTC share to combined together. 10,000 times the amount of NBT sent in redemption order
 will be interpreted as the number of BearBTC share and BullBTC share user would like to cash out. The formula is as follow:

```
the valid number of share in redemption = MIN ( the number of BearBTC share in holding, the number of BullBTC share in holding, 10000 * amount sent in redemption order )
the amount of cash out = the valid number of share in redemption * ( NAV of ET BearBTC + NAV of ET BullBTC )
```

- Example of a Nubits transaction:

> input:
> - Bxxxxxxxxx , ...
> - Byyyyyyyyy , ...

> output:
> - BBearBTCaddr, 0.1
> - Bzzzzzzzzzzz, ....
 
> Assuming UserAddr Bxxxxxxxxx is holding 2000 share of BearBTC and 1200 share of BearBTC, then 1000 share of BearBTC and 1000 share of BullBTC will be cash out. 
Given the NAV of BearBTC is 1.1 and the NAV of BearBTC is 0.9, 2000 NBT will be sent to UserAddr Bxxxxxxxxx.


## - Transfer Pool share to another user

To submit a Pool share transfer order, user send a certain amount of NBT from UserAddr to BearBTC or BullBTC share address and 0.0001 NBT to receiver's address in one Nubits transaction. 
The transfer order will be processed every minute. 10,000 times the amount of NBT sent in redemption order will be interpreted as the number of BearBTC share and BullBTC share user would like to send out. The formula is as follow:

```
the number of share sent = MIN ( the number of BearBTC / BullBTC share in holding, 10000 * amount sent in redemption order )
```

- Example of a Nubits transaction:

> input:
> - Bxxxxxxxxx , ...
> - Byyyyyyyyy , ...

> output:
> - BBullBTCaddr, 0.1
> - Bzzzzzzzzzzz, 0.0001
> - Bsssssssssss, ....
 
> Assuming UserAddr Bxxxxxxxxx is holding 1200 share of BearBTC, then 1000 share of BullBTC from UserAddr Bxxxxxxxxx will be transferred to UserAddr Bzzzzzzzzzzz. 

# Part 2: On Exchange Interface

## - Deposit

To make a cash deposit, user send 100 or more NBT from UserAddr to ExchangeBuy or ExchangeSell address. The send-from address
will be registered as UserAddr in NuLagoon. The formula is as follow:

```
the number of share sent = MIN ( the number of BearBTC / BullBTC share in holding, 10000 * amount sent in redemption order )
```

- Example of a Nubits transaction:

> input:
> - Bxxxxxxxxx , ...
> - Byyyyyyyyy , ...

> output:
> - ExchangeBuyAddr, 200
> - Bsssssssssss, ....
 
> 200 NBT will be credit to UserAddr Bxxxxxxxxx 's cash account. 


## - Buy / Sell Orders

To submit a buy or sell order, user send a certain amount of NBT from UserAddr to BearBTC / BullBTC share address and ExchangeBuy / ExchangeSell address in one Nubits transaction.
10,000 times the amount of NBT sent to BearBTC / BullBTC share address will be interpreted as the size of share user would like to buy / sell. 1,000 times the amount of NBT sent 
to ExchangeBuy / ExchangeSell address will be interpreted as the price of share user would like to buy / sell. The formula is as follow:

```
the valid number of share to sell  = MIN ( the number of share in holding, 10000 * the amount sent to BearBTC / BullBTC share address )
the valid number of share to buy  = MIN ( the amount of cash in holding, ( 10000 * the amount sent to BearBTC / BullBTC share address ) / (1,000 * the amount sent to ExchangeBuy / ExchangeSell address ) )
```

- Example of a Nubits transaction:

> input:
> - Bxxxxxxxxx , ...
> - Byyyyyyyyy , ...

> output:
> - BBullBTCaddr, 0.1
> - ExchangeSellAddr, 0.1231
> - Bsssssssssss, ....
 
> Assuming UserAddr Bxxxxxxxxx is holding 1200 share of BullBTC, then the exchange order book will indicate that UserAddr Bxxxxxxxxx want to sell 1000 share of BullBTC at the price of 1.231. 

- Example 2 of a Nubits transaction:

> input:
> - Bxxxxxxxxx , ...
> - Byyyyyyyyy , ...

> output:
> - BBearBTCaddr, 0.1
> - ExchangeBuyAddr, 0.1231
> - Bsssssssssss, ....
 
> Assuming UserAddr Bxxxxxxxxx is holding 1200 NBT in cash account, then the exchange order book will indicate that UserAddr Bxxxxxxxxx want to buy 974.81 share of BearBTC at the price of 1.231. 

## - Cancel Orders

To submit a cancel order, user send a certain amount of NBT from UserAddr to BearBTC / BullBTC address and 0.0011 NBT to ExchangeBuy / ExchangeSell share address in one Nubits transaction.. 
10,000 times the amount of NBT sent to BearBTC / BullBTC address will be interpreted as the size of order user would like to cancel. The orders which are closer to the the middle price on 
order books will have higher priority to be canceled. 

```
the amount of cash withdraw = MIN ( the amount of cash in holding, 10000 * amount sent in redemption order )
```

- Example of a Nubits transaction:

> input:
> - Bxxxxxxxxx , ...
> - Byyyyyyyyy , ...

> output:
> - BBearBTCaddr, 0.1
> - ExchangeBuyAddr, 0.0011
> - Bsssssssssss, ....
 
> Assuming UserAddr Bxxxxxxxxx is buying 1000 share of BearBTC at price 1.1 and buying another 500 share at price 1.2 in exchange order book, then order buying 1000 share at price 1.1 will be canceled. 


## - Withdraw 

To submit a withdraw order, user send a certain amount of NBT from UserAddr to ExchangeBuy or ExchangeSell address. 10,000 times the amount of NBT sent in withdraw order
 will be interpreted as the amount of cash user would like to withdraw. The formula is as follow:

```
the amount of cash withdraw = MIN ( the amount of cash in holding, 10000 * amount sent in redemption order )
```

- Example of a Nubits transaction:

> input:
> - Bxxxxxxxxx , ...
> - Byyyyyyyyy , ...

> output:
> - ExchangeBuyAddr, 0.11
> - Bsssssssssss, ....
 
> Assuming UserAddr Bxxxxxxxxx is holding 1200 NBT in cash account, then 1100 NBT will be sent to UserAddr Bxxxxxxxxx. 


# Part 3: NAV Calculation

## - NAV of ET Pool

The fund in ET pool, which is not including fund in users' exchange cash account, will work together with NuLagoon Pool A, C, D. The percentage movement of NAV of ET Pool
 will be exactly same as that of NAV of Pool A.  

```
Total asset = the amount NBT + the amount of BTC * BTC price + custodian fee - manage fee
NAV of ET Pool today  = NAV of ET Pool yesterday * total asset today / total asset yesterday
```

## - NAV of BearBTC 

BearBTC is moving at inverse direction of BTC price with exact 2 times leverage 

```
NAV of BearBTC today = NAV of BearBTC yesterday * 2 * ( 1 - BTC price today / BTC price yesterday )
```

## - NAV of BullBTC

BullBTC is moving at same direction of BTC price with approximate 2.5 times leverage 

```
NAV of BullBTC today = 2 * NAV of ET Pool today - NAV of BearBTC today
```

## - Dividend payment and NAV adjustment

When NAV of BearBTC is 5 times (or more) of NAV of BullBTC, the dividend payment and NAV adjustment will be triggered. The number of both BearBTC and BullBTC shares will shrink
 ( 1 / NAV of BearBTC ) times, and the NAV of them will be set at 1 again. In addition, a certain number of BearBTC and BullBTC shares will be paid to BearBTC holders as a dividend.
Same procedure applies when the BullBTC worth 5 times than BearBTC. The value of users' holding doesn't change after the dividend payment and NAV adjustment.

```
the NAV of BullBTC / BearBTC shares after adjustment = 1
the number of BullBTC / BearBTC shares after adjustment = the number of BullBTC / BearBTC before adjustment * the less NAV of BullBTC and BearBTC before adjustment
the number of BullBTC / BearBTC shares as dividend = (the greater NAV of BullBTC and BearBTC - the less NAV of BullBTC and BearBTC) * the number of shares of instument which has greater NAV /2 
```

- Example of dividend payment and NAV adjustment:

> NAV before adjustment
>  - BearBTC: 0.4
>  - BullBTC: 2.0
>  - Pool ET: 1.2

> Holding before adjustment
>  - User A: 1000 shares of BearBTC, Value = 400
>  - User B: 1000 shares of BullBTC, Value = 2000

> NAV after adjustment
>  - BearBTC: 1
>  - BullBTC: 1
>  - Pool ET: 1

> Dividend payment
>  - User A: None
>  - User B: 800 shares of BullBTC + 800 shares of BearBTC

> Holding after adjustment
>  - User A: 400 shares of BearBTC, Value = 400
>  - User B: 400 shares of BullBTC + 800 shares of BullBTC + 800 shares of BearBTC, Value = 2000
