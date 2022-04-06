# Interface

#### ID interface 

An interface to be implemented by any type that servers as an identifier for another object/s.  

ID interface{

    // String returns representation of the ID in a human redable string 
	String() string

    //Bytes return the byte array of the ID 
	Bytes() []byte

    // Compare takes an ID to be compared with and compares the ID returning the innteger difference between the bytes of the indentifier, for sorting/matching
	Compare(ID) int
}

#### NFT interface

A bare bone interface to be implemented by any structure that can be classified as an NFT 

NFT interface {

    // ID returns the identfier for the NFT as an ID interface
	ID() ID
	
	// ClassificationID returns the classification/type/denomination for the NFT as an ID interface
	ClassificationID() ID
}

#### NFT Wallet interface

A basic interface for a wallet for structures implementing the `NFT` interface

NFTWallet interface {
    // AccountAddress returns the accountAddress of the account which the NFTWallet belongs to
	AccountAddress() AccountAddress
	
	// NFTIDs returns the identifier, for all the NFTs stored in the wallet, as an ID interface
	NFTIDs() []ID
}

####  InterNFT interface 

An interface that implements the NFT interface, adding interoperability functionalities to it 

InterNFT interface {

    // Implementing the NFT interface
    NFT

    // ChainID returns the idendtifier, for the NFT's native Chain, as an ID interface
	ChainID() ID
    
    // HashID return the indentifier, for the immutable properties of the InterNFT, as an ID interface
	HashID() ID
    
    // MaintainersID returns the indentifier, for the mainainer froup of the InterNFT, as an ID interface
	MaintainersID() ID

    // Properties returns the properties of the interNFT as a properties interface
	Properties() Properties
    
    // CanSend returns a boolean telling if the interNFT can be sent or not given the current height
	CanSend(Height) bool

    // CanBurn returns a boolean telling if the interNFT can be burnt or not given the current height
	CanBurn(Height) bool
}

#### Height interface

An interface to define a block height type for a chain, used as a metric of time.

{
    Height interface {
    
    // Count returns the block count for the Height
	Count() string

    //Current height 
    // IsGraterThat returns a Boolean to tell if the Height is grater than a given Height/Current Height
	IsGraterThat(Height) bool
}

#### Signature interface 

An interface for any type that represents a cryptographic signature that can be verified

Signature interface {
    
    // String returns the human redable string format of the Signature
	String() string
	
	// Bytes returns the byte array of the cryptographic signature 
	Bytes() []byte
    
    // ID returns the identifier for the Signature as an ID interface
	ID() ID
	
	// Verify returns a boolean to tell if the signature is valid of not given the public key of the signer and the signed bytes
    Verify(PublicKey, []byte) bool
    
    // HasExpired returns a boolens to tell if the Signature has expired given a Height/Current Height interface
    HasExpired(Height) bool
}

#### Signatures interface 

An interface for a container of a collection of Signatures. The Interface handles the deterministic operations on the Signature collection.  

Signatures interface {
   
    // Get returns a Signature stored in the Signatures given an Identifier for it
	Get(ID) Signature

    // Add appends a given Signature with the Signatures Collection
	Add(Signature) error
	// Add removes a given Signature from the Signatures Collection
	Remove(Signature) error
	// Add mutates a given Signature in the Signatures Collection
	Mutate(Signature) error
}

#### Fact interface 

An interface to define a type for any kind of information is the system which is non-consequential to the application logic but has to be stored for provinance. 

Fact interface  {

    // String returns the human readable string format of the information stored by the Fact
	String() string
	
	// Bytes returns the byte araay of the information contained by the Facr
	Bytes() []byte

    // Signatures return the cyptographic signatures on the Fact as Signatures interface 
	Signatures() Signatures
}

#### Property interface

An interface to define any kind of property associated with an interNFT

Property interface {
    
    // Name returns the name of the Property
	Name() string
    
    // ID returns the indetifier, of the Property, as an ID interface
	ID() ID
	
	// Fact returns the Fact associated with the Property
	Fact() Fact
}

#### Properties interface 

An interface for a container of a collection of Properties. The Interface handles the deterministic operations on the Property collection.  

Properties interface {
    
    // ID returns the indetifier, of the Properties, as an ID interface
	Get(ID) Property

    // Add appends the given Property with the Properties collection 
	Add(Property) error
	// Add removes the given Property from the Property collection
	Remove(Property) error
	// Add mutates the given Property in the Property collection
	Mutate(Property) error
}

#### Properties interface 

An interface for any type of Trait associated with a Classification of interNFT 

Trait interface {

    // Name returns the name of the Trait
	Name() string
	
	// ID returns the identifier, for a Trait, as an ID interface
	ID() ID

    // IsMutable returns a Boolean to tell if a property value of Trait can be mutated or not
	IsMutable() bool
}

#### Traits interface 

An interface for a container of a collection of Traits. The Interface handles the deterministic operations on the Trait collection. 

Traits interface {

    // Get returns a Trait for the given ID
	Get(ID) Trait
}

#### Classification interface 

An interface for a representation of type/class/denomination of the interNFT

Classification interface {

    // Name returns a human redable name for the classification
	Name() string

    // ID return the identifier, for the classification, as an ID interface
	ID() ID
    
    // Traits returns the traits associated with the Classification
	Traits() Traits
}