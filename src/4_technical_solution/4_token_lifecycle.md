# NFT life cycle

![Mint Diagram](../image/technical_diagrams/Watermark%20NFT-Ownership-chain.drawio.png)

Once minted, a basic ERC721 token for example can be sold and re-sold several times. During the sale, there is an ownership token transfer between the previous owner and the new owner in exchange for some form of currency (fiat, crypto, etc.). In the real world, when an asset is sold, the two stakeholders sign a contract certifying the two steps of the process. First, the seller transfers the token ownership of the targeted asset and second, the buyer certifies the beginning of his ownership of the asset.

## Two Steps Sale

With our Watermark NFT contract, this two steps process translates to similar digital actions on the blockchain network. First the current token owner transfers the ownership of the token to the new owner, by using the existing smart contract function. For the first steps nothing changes compared to classical NFT norms (e.g., ERC-721).

For the second step there are a lot of changes compared to existing NFT norms. Most importantly, in the existing NFT ecosystem there is only one step, the token ownership transfer and that’s it. There is no second step of the new token ownership certification. The new owner just “receives” the token without having to sign or input something in the blockchain. But for a Watermark NFT, a new ownership certification must take place by the new owner by “asserting” the event on the blockchain. The new owner needs to perform a new steganography process with new ownership meta-data.

### Ownership Meta-data content

The new ownership meta-data contain:

- the new owner’s public key
- the owner counter/index incremented by +1
- the same blockchain network ID or another ID if the token transfer is cross-chain (inter-chain bridges, sidechains, etc.)
- a new transaction hash (this time the TX hash not from the mint transaction by from the token ownership transfer transaction)
- a new parent file hash (the previous stegano hash and not the genesis hash)

### Optional values in Ownership Meta-data

For the storage variable values, it is still optional and up to the developer to decide to include it or not. But the chosen set of storage variables need to be consistent all along the chain of ownership. If storage variables A, B and C are chosen, at index N the same variables need to be included. The inputted values must be the storage variable values at the block number of the ownership transfer transaction hash specified by TX hash.

### Example: NFT of Instagram Post

For instance, we imagine the token represents an Instagram post with likes and shares as storage variables evolving over time. The developer decides to include the likes storage variable in the steganography. The owner index 7 sells the NFT to a new owner index 8. At the time of the ownership transfer (block number X to be specific), the like storage variable has a value of 3000. When the new ownership certification by the new owner index 8 takes place, the likes could be at 3005. But the storage variable value that will be included must be 3000 and not 3005, because the ownership transfer appended when the storage variable had a value of 3000. Moreover, the specified TX hash (cryptographic hash of the token ownership transfer) refers to a block number where the like storage variable had a value of 3000.

Including the parent file hash (previous stegano hash) in the meta-data creates a chain of ownership secured by a robust cryptography algorithm that is the hash function. This reproduces the base concept of the blockchain technology by including the hash of the previous element in the current element meta-data. We have a unique chain of ownership for a single token. The File-Ownership-Chain.

The new ownership meta-data must be signed by the new token owner using his private key (the same private key to the address owning the said token). The resulting signature certifies the new ownership by the current owner by stating that the owner recognizes there has been a token ownership transfer from a previous blockchain address to his current address. “I, Alice, certify that I received a token from this address, with those current ownership meta-data (TX hash, parent file hash, etc.).”

Once the new ownership meta-data is signed, both it and its signature must be combined to produce the new stegano meta-data. The stegano meta-data is to be embedded in a new stegano file. The new stegano file is the combination of the genesis file and the new stegano meta-data. For each new owner certification, the steganography process must be done using the genesis file. Once the steganography process is done, the file also needs to be stored on a permanent storage.

Finally, the new token owner needs to input the new stegano hash and the new token URL on the smart contract. Once done, the new token ownership has been certified and the step 2 is complete.

### Summary

To summarize, we have two steps in the token `ownership` transfer. The first step is carried out by the current owner. The token owner’s public key is updated on the smart contract. The second step is carried out by the new owner. The new owner signs the new ownership meta-
data, embed it in a new stegano file, store the new stegano file on the permanent storage and input the stegano hash and its location on the smart contract.

If we compare this new process to the existing process, step 1 is already in place in existing NFT norms. The new component is step 2 which includes a compulsory input on the blockchain from the new token owner. The two steps process mimics the real life process of an asset ownership transfer. So, compulsory input is more accessible by humans because the real world already imposes this process.

For the new owner to be able to re-sell the token, the new ownership certification must have been carried out, otherwise the token must not be able to be transferred. It is compulsory to include this rule in the smart contract otherwise it would break the chain of ownership. There must be a security mechanism preventing the sale of the token so long as the new ownership certification has not been carried out.

## File-Ownership-chain

The schema shows a chain of ownership depicting the ownership status of a single token. Each element is a unique ownership instance of the token. This is the same concept as a chain of blocks (blockchain), hence the name Ownership-Chain.

### Parent File Hash

The Ownership-Chain is a chain of files. Each file is connected to the previous file through the previous file’s hash value. Each file contains the hash value of the previous (also called parent) file embedded in its data using steganography. The parent file hash refers to the hash of the previous file in the chain of ownership. The parameter “parent file hash” in the ownership meta-data contains the previous hash and is responsible for the cryptographic chain, just like the parameters “parent hash” inside a block of a blockchain.

### Mathematical Series of length N

Each stegano file has its index which is a positive integer. When dealing with a specific stegano file, we use the term “stegano file index i” (like a mathematical series) or the “N stegano file”. By extension we name each stegano hash the stegano hash index i or “i stegano hash”. Each ownership meta-data has its index which is also a positive integer, also called ownership meta data index i (i ownership meta-data). The ownership meta-data index 1 corresponds to the stegano file index 1 and meta-data index i corresponds to the stegano file index i.

### Stegano File index i

Each stegano file is the combination of the genesis file (genesis file is `index 0`) and of the ownership meta-data index i (each a unique element).

Each N ownership meta-data is signed by the owner index N and generates the stegano meta-data index N:

i ownership meta-data + its signature by owner index i = i stegano meta-data

The the meta-data index `i` must be embedded in the Genesis file (file index 0).

### Ownership index i

Each element in the Ownership-chain is called ownership index i corresponding to meta-data index i and stegano file index i. The ownership 1 is called the genesis ownership (≠ genesis file, which is index 0). There is no ownership index 0, nor meta-data, nor stegano file index 0. The index 0 is reserved for the genesis file. If we look at the Ownership-Chain through a mathematical perspective, it’s a pseudo mathematical series with an initial value at index 0 (genesis file) and going through each positive integer by `i+1` (i = current index) increment and of length N.
