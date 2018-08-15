Smart Contract
=======

All of Totle is powered by a Smart Contract at it's core, that executes a series of buys or sells against the multiple DEXes we support.

contract address
---------

Our contract address is currently ``0xd94c60e2793ad587400d86e4d6fd9c874f0f79ef``. Note that the most up-to-date contract address is returned by the Suggestor API.


abi
----------------

Our ABI is currently ``[{"constant":true,"inputs":[],"name":"owner","outputs":[{"name":"","type":"address"}],"payable":false,"stateMutability":"view","type":"function"},{"constant":false,"inputs":[{"name":"handler","type":"address"},{"name":"allowed","type":"bool"}],"name":"setHandler","outputs":[],"payable":false,"stateMutability":"nonpayable","type":"function"},{"constant":false,"inputs":[{"name":"tokenAddresses","type":"address[]"},{"name":"buyOrSell","type":"bool[]"},{"name":"amountToObtain","type":"uint256[]"},{"name":"amountToGive","type":"uint256[]"},{"name":"tokenForOrder","type":"address[]"},{"name":"exchanges","type":"address[]"},{"name":"orderAddresses","type":"address[8][]"},{"name":"orderValues","type":"uint256[6][]"},{"name":"exchangeFees","type":"uint256[]"},{"name":"v","type":"uint8[]"},{"name":"r","type":"bytes32[]"},{"name":"s","type":"bytes32[]"}],"name":"executeOrders","outputs":[],"payable":true,"stateMutability":"payable","type":"function"},{"constant":true,"inputs":[{"name":"","type":"address"}],"name":"handlerWhitelist","outputs":[{"name":"","type":"bool"}],"payable":false,"stateMutability":"view","type":"function"},{"constant":true,"inputs":[],"name":"MAX_EXCHANGE_FEE_PERCENTAGE","outputs":[{"name":"","type":"uint256"}],"payable":false,"stateMutability":"view","type":"function"},{"constant":false,"inputs":[{"name":"newOwner","type":"address"}],"name":"transferOwnership","outputs":[],"payable":false,"stateMutability":"nonpayable","type":"function"},{"inputs":[{"name":"proxy","type":"address"}],"payable":false,"stateMutability":"nonpayable","type":"constructor"},{"payable":true,"stateMutability":"payable","type":"fallback"},{"anonymous":false,"inputs":[{"indexed":true,"name":"previousOwner","type":"address"},{"indexed":true,"name":"newOwner","type":"address"}],"name":"OwnershipTransferred","type":"event"}]``. 

Note that you can find the current ABI by searching the contract address returned by the Suggestor API on Etherscan and clicking on the 'Code' section,


executeOrders
-------------

Note that the returned values of the Suggestor API includes all of the Smart Contract executeOrders paramaters you need to get the best bid/ask orders for your token in the orders object. 

The executeOrders endpoint of the Smart Contract takes the following parameters:

tokenAddresses (address[]) - the token address at the trades level

buyOrSell (bool[]) - are you buying or selling, array

amountToObtain (uint256[]) - how much Eth/tokens you're looking to get, array

amountToGive (uint256[]) - how much Eth/tokens you're looking to supply, array

tokenForOrder (address[]) - the token address at the orders level. The reason that the tokenForOrder was added was so that we could make sure that each “order” was for the correct token and easily spot problems if the payload was incorrect.

exchanges (address[]) - which exchanges to execute the orders against, array

orderAddresses (address[8][]) - the addresses of the orders, array

orderValues (uint256[6][]) - the total values of the orders, array

exchangeFees (uint256[]) - the fees on the exchanges, array

v (uint8[]) - the v value of the signed hashes, array

r (bytes32[]) - the r value of the signed hashes, array

s (bytes32[]) - the s value of the signed hashes, array