totle
====================


Usage
-----

Introducing the Totle API and Smart Contract, interacting together to give you the control and automation of working with the most popular DEXes!

How does it work?

In the present version of the API + Smart Contract

Query the graph endpoint on the site with your address and a Graph QL query to see if the token exists, and other potential variables like change 1hr, change 24hr, volume

var req = {
            "operationName": null,
            "variables": {
                "address": d.tokenAddr
            },
            "query": "query ($address: String) {\n  token(address: $address) {\n    address\n    name\n    price\n    priceChange {\n      change1h\n      change24h\n      change7d\n    }\n    bestPrice {\n      bid\n      ask\n    }\n    orders {\n      asks {\n        price\n        volume\n        exchangeId\n      }\n      bids {\n        price\n        volume\n        exchangeId\n      }\n    }\n    exchanges\n  }\n}\n"
        }

Returns a set of data with useful info:

{ address: '0xff3519eeeea3e76f1f699ccce5e23ee0bdda41ac',
  name: 'BCAP',
  price: null,
  priceChange: { change1h: null, change24h: null, change7d: null },
  bestPrice: { bid: 0.004, ask: 0.0048889 },
  orders: 
   { asks: 
      [ [Object],

Query the Suggestor API with token address + amount to spend to receive the set of variables to pass the Smart Contract

Returns the exact info to provide the smart contract, and Eth Value to send (under orders[0] to orders[11]):

{ success: true,
  response: 
   { ethValue: '1589957762130999993086',
     summary: { buys: [Array], sells: [] },
     orders: 
      [ [Array],
        [Array],
        [Array],
        [Array],
        [Array],
        [Array],
        [Array],
        [Array],
        [Array],
        [Array],
        [Array],
        [Array] ],
     contractAddress: '0xd94c60e2793ad587400d86e4d6fd9c874f0f79ef' } }


Use an Eth interface like Web3 to interact with the Smart Contract using (or by modifying) the supplied variables. For buying tokens you just need to use the executeOrders endpoint of the smart contract, otherwise for selling be sure to approve the amount with the token contract’s approve function first!

In our soon-to-be-released updates, you’ll be able to pass the Suggestor inclusion/exclusion criteria, acceptable slippage %, and backup orders. We’re constantly reiterating to make the product more usable.

Interested in having a percent of our fees once we’re out of beta by integrating your product or service with our API? ICOs looking to token swap or Eth swap, exchanges looking for increased liquidity? Contact Us Here to express interest, and our developer advocate will respond to you quickly!

.. toctree::
   graphql
   suggestor
   smartcontract