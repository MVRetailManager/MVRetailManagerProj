# MVInventoryChain Minimum Viable Product (MVP)
The main blockchain component of the MVRetailManagement system

## MVP Features
### Basics
Initially the basics of a blockchain should be implemented, with the ability to store transactions on the blockchain, generate wallets, mine blocks, and create new blocks and distribute tasks over a decentralised destributed network.

### Items
Each item will be stored under its "UPC" code, along with a corresponding "Friendly Identifier" (from https://www.barcodelookup.com/api), expiry, and its value

Each block will also contain a quantity, the user comitting the block, and the bin location

### Orders
When item counts run low the network should generate orders which can be sent to suppliers to replace those items
NB: For the MVP orders will simply order enough to replenish each by the exact number of items sold, and these orders will be placed when *sales > items remaining*
Order blocks will contain:
* A delivery manifest (see deliveries below) of all the desired items
* A desired delivery date for **each** item

### Deliveries
Deliveries can be used as coinbase transactions to add items into the network when they arrive in store, these can then be allocated to a bin (see below) or area on the shop floor for further movements and transactions
When a delivery is completed any unspent orders that have been delivered during that delivery should be removed
Delivery blocks will contain:
* A manifest of all items within the delivery (see items for details on what is stored on items)
* An estimated delivery time
* A delivery "department" which can be used to allocate the correct staff to the delivery - e.g. "FROZEN" for frozen goods, or "CHILLED" for chilled goods, etc

### Bins
Bins can also be committed to the chain, edited or updated through comitting a block to the network.
Bin blocks will contain:
* The bin code (unique identifier which can be formatted as a barcode for that bin)
* Bin's friendly identifier
* Bin description

### Wastage
Wastage blocks will inform the network that an item has been thrown away, and have a negative effect on the "Network score"
Wastage blocks will contain:
* The UPCs of the items wasted
* The quantity of each item wasted
* The user committing the wastage block
* Total value of waste

### General Removal
General removals will act in the same way as wastage in removing/"burning" the item from the blockchain, however, this will be used for things such as selling the item, or for the purpose of correcting human error
General removal blocks will contain:
* The UPCs of the items removed
* The "rationale" for removal - this will be an enumerator 
* The user comitting the removal
* Total value of the removal

## MVP Implementation
The MVP will be implemented in Go attemtping to recognise and follow all relevant open source go standards.
For the purposes of the MVP, the front end for interaction will be implemented through a command line interface (CLI)