---
title: "Redpoint API"
date: 2022-12-18T10:30:55-05:00
description: "Cosmos MEV simulator."
page_header_bg : "images/bg/section-bg5.jpg"
image: "images/portfolio/redpoint.png"
author: "Kyle Moser"
draft: true
comments: true
categories: 
  - "Cosmos"
tags:
  - "DeFi"
  - "Taxes"
---


>Redpoint is a service that simulates trades on compatible DEXs and provides the operator with information to maximize trades and capture arbitrage. Redpoint allows a trader (e.g. DEX front end, or wallet) to simulate a trade *before submitting it on chain*. Redpoint is a JSON REST API.<br><br> 

## How does the service maximize rates?

The Redpoint API discovers all possible routes on the DEX, simulates the trade for the most likely routes (based on total fees, spot price, and slippage), and chooses the route with the greatest return. Additionally, if any arbitrage results from the user's trade, Redpoint will provide the correct swap that will capture that arbitrage profit.
> **_NOTE:_**  If preferred, Redpoint allows the trader to specify the exact routes/token amounts.

## What is arbitrage?

Generally speaking, large trades result in high slippage. The user's trade suffers since they are not receiving the maximum possible price. Typically, on Cosmos based DEXs, trading bots wait for these high slippage transactions to unbalance a liquidity pool, creating a profit-making opportunity. Bots race to rebalance the DEXs' pools, making themselves a [profit in the process](https://www.mintscan.io/osmosis/txs/860696A09439B6DA4E4B4D71BCA2FCED1EC1F5C61AD695FD450D9B562C3C9F8F).

## How does Redpoint benefit customers by capturing arbitrage?

Redpoint simulates the user's trade and figures out how much arbitrage will be caused by the user's trade. Redpoint figures out the exact "counter-trade" to capture that arbitrage. These trades can be [packaged into a single Cosmos TX](https://www.mintscan.io/osmosis/txs/01FDE16DFA1B27A381A2494E76E4EB78A4B0978849F88E16C53C7A32A6E81E94), ensuring that the operator (user) benefits from the arbitrage, not trading bots.  

### Example trade simulation

The DEX front end or wallet asks the Redpoint API “How should my user trade 3,500 OSMO for AKT"? The API responds with: 

1. Trade 3,500 OSMO using pool 3  
1a. This will result in 15,080 AKT
2. Trade 793.55 OSMO through pools 1,4,3.  
2a. This results in 796.23 OSMO, a profit of 3 OSMO.  

![Example](./img/redpoint-arb-example-1.png)
<figcaption><b>One TX</b> with <b>two messages</b>, made possible with Redpoint</figcaption>  

&nbsp;  
There are several ways the trades can be submitted to the chain. 

1. As above, a single TX can be submitted containing two swap messages. This ensures the trader captures the arbitrage.  
1a. In this scenario, authz can be used to allow a specific wallet to perform the arbitrage trade.  
1b. Furthermore, feegrants can be used so that the user pays the fee, not the trading platform.
2. Two separate TXs can be submitted, one with the user trade and one with the arbitrage trade.  
2a. To prevent racing with bots, or frontrunning attacks, Mekatek or Skip must be used in this case (see below).

## Is Redpoint different than Mekatek/Skip?

Mekatek and Skip offer services to searchers - for example, an arbitrage bot could purchase favorable block placement to ensure their TXs are given priority in a block, or to ensure two transactions are executed one after another. Redpoint is complimentary to these services. For example, consider the example trade simulation above. One option is to submit a single TX with two messages, ensuring the user's swap and arbitrage swap are package together (and guaranteeing the arbitrage profits are captured). A second option is to use Mekatek's or Skip's services to submit the user's trade and arbitrage trade one after another on-chain, ensuring the arbitrage is captured by the desired wallet.

## CLI tool 

Redpoint is an information provider, not a trading front-end. We have [many examples](https://www.mintscan.io/osmosis/txs/663745663E94DD58814068BFF6EA2945BD6C2D9153239A6F02C24225AAE151E1) of real trades, performed as a proof of concept with our [CLI tool](https://github.com/DefiantLabs/defiant-swap). Potential partners can use our CLI tool to demonstrate how our tool could integrate with their platform. Partners can easily verify that our API works by comparing trades on the Osmosis front-end to trades with our CLI tool. Note: our CLI tool is able to do simulations as well as execute trades. 

### JSON request/response formats

Our CLI tool (written in Go) is the best way to become familiar with our API. We also have swagger documentation available by request and we are working on a Javascript API.

Example request to our API:

```json
{
  "ArbitrageWallet": "osmo14mmus5h7m6vkp0pteks8wawaj4wf3sx7fy3s2r",
  "SkipWalletFundsCheck": true,
  "TokenInAmount": "10000",
  "TokenInSymbol": "AKT",
  "TokenOutMinAmount": "1",
  "TokenOutSymbol": "OSMO",
  "UserWallet": "osmo1njsthsamgkzdqqg4awj7y6rxtuk3q26t2t8md2"
}
```
API response:
```json
{
  "HasArbitrageOpportunity": true,
  "userSwap": {
    "TokenIn": {
      "denom": "ibc/1480B8FD20AD5FCAE81EA87584D269547DD4D436843C1D20F15E00EB64743EF4",
      "amount": "10000000000"
    },
    "TokenOutMinAmount": "1000000",
    "Pools": "3",
    "routes": [
      {
        "pool_id": 3,
        "token_out_denom": "uosmo"
      }
    ],
    "TokenOutAmount": "2367541223",
    "TokenOutDenom": "uosmo",
    "TokenInSymbol": "AKT",
    "TokenOutSymbol": "OSMO",
    "AmountOutHumanReadable": "2367.541223 OSMO",
    "BaseAmount": "2367.541223",
    "PriceImpact": 0.003323
  },
  "arbitrageSwap": {
    "SimulatedSwap": {
      "TokenIn": {
        "denom": "uosmo",
        "amount": "398727188"
      },
      "TokenOutMinAmount": "398727188",
      "Pools": "3,4,585,584",
      "routes": [
        {
          "pool_id": 3,
          "token_out_denom": "ibc/1480B8FD20AD5FCAE81EA87584D269547DD4D436843C1D20F15E00EB64743EF4"
        },
        {
          "pool_id": 4,
          "token_out_denom": "ibc/27394FB092D2ECCD56123C74F36E4C1F926001CEADA9CA97EA622B25F41E5EB2"
        },
        {
          "pool_id": 585,
          "token_out_denom": "ibc/0954E1C28EB7AF5B72D24F3BC2B47BBB2FDF91BDDFD57B74B99E133AED40972A"
        },
        {
          "pool_id": 584,
          "token_out_denom": "uosmo"
        }
      ],
      "TokenOutAmount": "399856273",
      "TokenOutDenom": "uosmo",
      "TokenInSymbol": "",
      "AmountOutHumanReadable": "399.856273 OSMO",
      "TokenOutSymbol": "OSMO",
      "BaseAmount": "399.856273",
      "PriceImpact": 0
    },
    "EstimatedProfitHumanReadable": "1.129085 OSMO",
    "EstimatedProfitBaseAmount": "1.129085"
  }
}
```

## Supported DEXs

Currently, Redpoint supports Osmosis and Junoswap DEX (REST API backend). Our CLI tool public release supports Osmosis, and we are working on a Junoswap CLI tool.


[docs](https://docs.defiantlabs.net/products/redpoint/)  

