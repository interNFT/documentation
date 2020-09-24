# Introduction

InterNFT is a natively implemented NFT structure for Blockchain applications that implement interoperability protocols. The interNFT is defined by a basic interface that any NFT structure has to implement to be called an interNFT. The ownership of interNFT is maintained by the interNFT wallet. The combination of interNFT and interNFT wallet allows the ownership of the interNFT to be exchanged across interoperable chains while the execution logic of the NFT is still maintained at the native chain.

## Salient Features 
**Division of responsibility**
The NFT functionality is split into two modules, the NFT, and NFT wallet modules. NFT module handles the mint, mutation, and burns logic with the NFT wallet module handling the ownership transfer transactions. Both modules can operate independently on different chains.

**Singular representation/instantiation**
The NFTs are addressed by the same hash of the immutable properties, enforcing singular representation/instantiation of NFT across chains.

**Singular wallet implementation**
NFT wallet module implements the wallet and transfers logic and is agnostic to other custom logic related to the NFTs allowing for a singular wallet implementation of all the NFT types. 

**Implementation flexibility**
The NFT module implements all the basic functional requirements of an NFT with no restrictions on the extension of the functionalities to account for more complex application logic, as long as the implementation satisfies the NFT interface.

**Reduced load on interchain protocol**
The two modules comprising the NFT functionality do no need to communicate with each other to sync the state at each transaction. They function pretty independently only with only a few transactions requiring inter-chain operability(interchain send, burn transactions).

**Commoditization**
All the NFTs are represented with a class or classification allowing for transactions to address NFTs though classes instead of direct addresses and hence allowing for NFT commoditization.

**Trusted minting, mutation and burn execution and Interoperability with private chains**
 The minting, mutation, and burn logic is implemented natively on the issuing chain and is always handled by the same chain instead of handing over the mutation logic to the recipient chain on NFT transfer to a different chain. This allows for private and privately validated chains to also exchange their NFTs with other chains while ensuring the execution environment trust and logic privacy(if required).

**Native implementation and interoperability**
The NFT module is implemented at the native chain application logic level instead of at the Smart Contract level, leveraging the chain’s native interoperability protocols to transfer NFTs between chains instead of permissioned bridge Smart Contracts.


## VS ERC721

The proposed NFT structure is implemented at the native chain code level rather than at the smart contract level making it more ephemeral. ERC721 is the most popular NFT standard in general. The standard is very well suited for smart contract-based applications running on a single chain. But there are some disadvantages to using the same in a multi-chain environment on which the proposed standard is designed to improve upon:

**NFT origin address (Rigid Design)**
*Problem*
An NFT itself is not meaningful when transferred to another chain. The invariants and operations related to the NFT may be hacked leading to a bunch of attack vectors(like duplication, double-spends). In the case of Ethereum, the NFT resides in it’s issuing contracts with the ownership being changed to a wallet address or smart contract by the contract itself. But in a multichain environment with separate chain states, this might not be possible.
*Solution*
In the proposed design the NFT always resides in the issuing chain state with the issuer chain logic issuing, mutating, or burning the NFT. The ownership of the NFT is transferred through a reference to the NFT, the NFT Address structure which records the address of the Issuer chain for look-up, a hash of the invariants, to ensure singular representation, and the class or classification of the NFT. The reference may be passed around between wallets on different chains and the Owner address being updated on the Issuing chain (to prevent double-spending).

**NFT wallet (Lower Visibility)**
*Problem*
One cannot directly query all the NFTs owned by their address in the ERC721 standard. The owner address has to be queried against the issuing-contract to get all the NFTs owned by the address. A new NFT assigned to a wallet may slip under the notice of the owner. In a multichain wallet scenario, the complexity of NFT tracking becomes amplified.
*Solution*
The proposed standard implements an NFT wallet where all the NFTs of different classes form all the Issuer chains can sit. The wallet can be queried against either the NFT address or the NFT class or get all the NFTs owned.

**Smart Contract vs Native implementation**
*Problem*
NFT transactions are heavier to execute because of the larger Byte volume that has to be modified on each transfer or mutation. This multiplied by the complexity of running the transaction logic on smart contracts increases the overall cost and reduces the TPS of NFT transactions. Also, ERC721 is known to have a defect where an NFT transferred to a contract that does not or incorrectly implements the on-received logic leads to the NFT getting lost irrecoverably and immutably.
*Solution*
The proposed solution implements the NFT transaction logic natively in the applications rather than on a smart contract running in an EVM or WASM execution environment, making the transactions much optimized, faster, and cheaper, also less prone to mistakes made by the smart contract implementers.

