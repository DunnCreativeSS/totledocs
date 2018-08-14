Graph QL
=======

GraphQL is a query language for our API (and other APIs) and a runtime for fulfilling those queries with our existing data.

Our GraphQL endpoint ``https://services.totlesystem.com/graph`` takes a number of optional paramaters and returns a number of optional response datas.

Note that the paramters sent to query are all optional, and can be defined inside the Graph QL query instead of as a variable.

This query represents every piece of data you can request, and is broken down into sections below:

.. code-block:: javascript

    {
       
    query ($address: String, $symbol: String, $networkId: [Int], $searchString: String) {
      exchanges {
        id
      }
      tokens ( symbol: $symbol, networkId:$networkId, searchString:$searchString) {
        name
        symbol
        address
        decimals
        iconUrl
        networkId
        color
        tradable
        price
        marketCap
        volume24h
      }
      exchangeRates {
        pair
        value
        date
      }
      token(address: $address, symbol: $symbol) {
        name
        symbol
        address
        decimals
        iconUrl
        networkId
        color
        tradable
        price
        marketCap
        volume24h
        bestPrice {
          ask
          bid
        }
        exchanges
        orders {
          asks {
            volume
            price
            exchangeId
          }
          bids {
            volume
            price
            exchangeId
          }
        }
        priceChange {
          change1h
          change24h
          change7d
        }
            
      }
    }
.. 

You can specify that only data should be returned that you request, and build a query that asks for the data you want:

.. code-block:: javascript


            "query": "query ($address: String) {
                token(address: $address) {
                    address
                    name
                    bestPrice {
                        bid
                        ask
                    }
                    orders {
                        asks {
                            price
                            volume
                            exchangeId
                        }
                        bids {
                            price
                            volume
                            exchangeId
                            }
                        }
                        exchanges
                    }
                }
            "
..

In Javascript, the query above would look like this:

.. code-block:: javascript

        var req = {
            "operationName": null,
            "variables": {
                "address": d.tokenAddr
            },
            "query": "query ($address: String) {\n  token(address: $address) {\n    address\n    name\n    bestPrice {\n      bid\n      ask\n    }\n    orders {\n      asks {\n        price\n        volume\n        exchangeId\n      }\n      bids {\n        price\n        volume\n        exchangeId\n      }\n    }\n    exchanges\n  }\n}\n"
        }


        request.post({
            url: 'https://services.totlesystem.com/graph',
            body: req,
            json: true
        }, function(error, response, body) {
            if (!error && response.statusCode == 200) {


            }
        }
..


exchanges
---------

``exchanges`` returns the ``id`` of all exchanges on Totle. This is an internal ID used in the other functions and features of Totle.

.. code-block:: javascript

    "data": {
        "exchanges": [
          {
            "id": 1
          },
          {
            "id": 2
          },
          {
            "id": 3
          },
          {
            "id": 4
          },
          {
            "id": 5
          }
        ]
        }

.. 

tokens
----------

``tokens`` can take the optional input variables ``symbol (String)``, ``networkId ([Int])``, ``searchString (String)``. It returns multiple tokens on the Totle platform per single query if there are multiple matches.

.. code-block:: javascript

    "tokens": [
          {
            "name": "OmiseGO",
            "symbol": "OMG",
            "address": "0xd26114cd6ee289accf82350c8d8487fedb8a0c07",
            "decimals": 18,
            "iconUrl": "https://s3.amazonaws.com/totle-token-icons/OMG-icon.png",
            "networkId": 1,
            "color": "#5fcbee",
            "tradable": true,
            "price": 0.013068693432351,
            "marketCap": 1827159.8270379,
            "volume24h": 192675.20050337,
            "bestPrice": {
              "ask": 0.0115,
              "bid": 0.012819100326229703
            },
            "orders": {
              "asks": [
                {
                  "volume": "1690000000000000",
                  "price": "1000.999999999999900000000000000000",
                  "exchangeId": 1
                }
                ,...
                ], "bids": [
                {
                  "volume": "32000000000000000000",
                  "price": "0.012819100326229703000000000000",
                  "exchangeId": 2
                },...
                ],
            },
            "priceChange": {
              "change1h": -1.07,
              "change24h": -17.33,
              "change7d": -36.28
            }
        }
.. 

``name`` is the English written name of the token.

``symbol`` is the ticker for the token.

``address`` is the token's contract address.

``decimals`` are the number of decimals the token has following the 0.

``iconUrl`` is an address where the token's icon is stored.

``networkId`` is the network where the token is active, 1 being mainnet.

``color`` is the color of the token.

``tradable`` is whether that token can be traded on Totle.

``price`` is the last price of the token among DEXes.

``marketCap`` is the token's market capitalization.

``volume24h`` is the token's aggregated 24 hour volume.

``bestPrice`` is an array containing the best ``ask`` and ``bid`` for the token among exchanges.

``orders`` is an array containing the aggregated orderbook, comprised of ``bids`` and ``asks`` which are in turn arrays built from the bid/ask ``volume``, ``price`` and ``exchangeId``.

``priceChange`` is an array made up of the token's price change in 1 hour ``change1h``, 24 hours ``change24h`` and 7 days ``change7d``.

token
------------------

``token`` can take the optional input variables ``address (String)``, or ``symbol (String)``. It returns a single token on the Totle platform per query if there is a match.

.. code-block:: javascript

    "token": {
      "name": "Student Coin",
      "symbol": "STU",
      "address": "0x0371a82e4a9d0a4312f3ee2ac9c6958512891372",
      "decimals": 18,
      "iconUrl": "https://s3.amazonaws.com/totle-token-icons/STU-icon.png",
      "networkId": 1,
      "color": "#4a0455",
      "tradable": true,
      "price": 0.000014779445202365,
      "marketCap": 715.08224249132,
      "volume24h": 112.09178512117,
      "exchanges": [
        1,
        3
      ],
      "bestPrice": {
        "ask": 0.00003855,
        "bid": 0.000010509
      },
      "orders": {
        "asks": [
          {
            "volume": "3000000000000000000",
            "price": "3.699999999999999700000000000000",
            "exchangeId": 1
          },...
          ],
        "bids": [
          {
            "volume": "990000000000000000000",
            "price": "0.000010509000000000000000000000",
            "exchangeId": 1
          },...
          ],
       },
      "priceChange": {
        "change1h": -3.89,
        "change24h": -16.78,
        "change7d": -31.89
      }
    }
.. 

``name`` is the English written name of the token.

``symbol`` is the ticker for the token.

``address`` is the token's contract address.

``decimals`` are the number of decimals the token has following the 0.

``iconUrl`` is an address where the token's icon is stored.

``networkId`` is the network where the token is active, 1 being mainnet.

``color`` is the color of the token.

``tradable`` is whether that token can be traded on Totle.

``price`` is the last price of the token among DEXes.

``marketCap`` is the token's market capitalization.

``volume24h`` is the token's aggregated 24 hour volume.

``bestPrice`` is an array containing the best ``ask`` and ``bid`` for the token among exchanges.

``orders`` is an array containing the aggregated orderbook, comprised of ``bids`` and ``asks`` which are in turn arrays built from the bid/ask ``volume``, ``price`` and ``exchangeId``.

``priceChange`` is an array made up of the token's price change in 1 hour ``change1h``, 24 hours ``change24h`` and 7 days ``change7d``.
