# Terminology

* `NFT`: An NFT or a Non-fungible Token is a structured unit of data that represents the properties of a unique entity, or the entity itself( if it’s a digital asset and all its properties are contained by the NFT). In this document `NFT` will also refer to a very basic interface, implementation of which will classify a structure as an `NFT`.

* `NFT ID`: A reference to the `NFT`. The address is convertible to a String for reference.

* `NFT Wallet`: an array of references(`NFT ID`) to Account ID.

* `NFT Classification ID`: an identifier of the type or denomination of the NFT.

* `interNFT`: An implementation of the `NFT` interface. The `interNFT` is defined to allow for maximum application logic flexibility in one interface and is focused on inter chain ownership transfer. In this document `NFT` will also refer to a very basic interface, implementation of which will classify a structure as an `NFT`

* `classification`: a representation of the type or grouping for an `interNFT`, e.g. an `asset` "Toyota Corolla" will be of `classification` car.

* `trait`: a charectersitic/variable related to an `asset` defined by `classification` e.g. "top speed" can be a `trait` of `classification` car.

* `signature`: a cryptographic signature using a private key on bytes of information. A signature can be verified against the public key of the signing private key and sign bytes.

* `fact`: a peice of information. A `fact` can carry `signature`s from `account`(s) e.g. "100 mph (ca. 161 km/h)" is a fact and an `account` can attest it by signing it with their private key.

* `property`: the value of a `trait` is `property`. Every `property` has a `trait` identifier and a corresponding fact `fact` e.g.

* `account`: a singularly identifiable identity of each actor on the application. An `account` is generally identified by a public key.

* `maintainers`: a group of one or more accounts that can issue and mutate `properties` of a `classification` of `interNFT`

* `interNFT wallet`: a mapping of a set of `interNFT ID`s against a `account` ID. A `interNFT wallet` signifies the `interNFT`s owned by and an account.

* `height`: the block height of the chain. Used as a measure of time for `interNFT` time bound operations.

* `lock`: the `height` after which the an `interNFT` is allowed to be transferred out of an `interNFT wallet`.

* `burn`: the `height` after which the an `interNFT` is allowed to be burned/redeemed by the owner of the `interNFT`.

* `interNFT ID`: A reference to the `interNFT` specifying the hash of the NFT Immutable, the address of the originating chain, and the class of the NFT. The address is convertible to a String for reference.

* `immutables`: `trait`s of the `interNFT` that do not change after issuing. The hash of these properties is a  part of the NFT Address( `interNFT ID`).

* `mutables`: `trait`s of the `interNFT` that can be changed through transactions defined on it.