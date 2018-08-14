Suggestor
=======

All of Totle is powered by a Smart Contract at it's core, that executes a series of buys or sells against the multiple DEXes we support.

inputs
---------

The Suggestor API is an endpoint for our API that returns suggested data to supply to the Smart Contract in order to achieve the best (highest/lowest) bids/asks for a supplied token.

Our Suggestor endpoint ``https://services.totlesystem.com/suggester`` takes a ``buys`` array or a ``sells`` array containing the ``token`` address and the total ``amount``, and the ``address`` of the Eth wallet that wants to trade.


In Javascript, the query would look like this:

.. code-block:: javascript

        var reqsells = {
            "sells": [{
                "token": token,
                "amount": total
            }],
            "address": "0x8ebA329784974b96EC6293DD83bf462651BB75E6"
        }
        request.post({
            url: 'https://services.totlesystem.com/suggester',
            body: reqsells,
            json: true
        }, function(error, response, body) {
            if (!error && response.statusCode == 200) {

            }

        }
..

outputs
---------

The Suggestor API returns an object like this:

.. code-block:: javascript

	{ success: true,
	  response: 
	   { ethValue: '1883786206306806040679',
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

.. 	     

The ``orders`` variable contains, in order, the variables you'd supply to the Smart Contract ``executeOrders`` function to get the best bid/ask prices for your total amount, as well as the ``ethValue`` to send the contract in order to execute.