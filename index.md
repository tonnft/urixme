# URIX: URIs, eXtensible

## Mint your names (with URIs) as NFTs on Matic
Unfortunately, we don't have UI/UX screen mock ups yet, but basically, there will be a web page where you can select a slug, check if it's still available, then add another slug, provide URI for each and mint them by one function call from a contract that extends ERC721URIStorage from OpenZeppelin. This way, we get a decentralised URI shortener service where every URI is treated as an NFT, with some bells and whistles.

**Testnet**: reserve any number of mappings (name=>URI) for free

**Mainnet**: if you prepay (with MATIC) the plasma needed to mass-mint your tokens, we call (after receiving batch of such prepayment transactions) a new function that mints everything, selected by a set of addresses. For this, we probably will deploy a testnet contract that receives (Mainnet) txId and, after verifying some kind of signature, reserves listed slugs/indices for Mainnet batch-minting...

This way everything valuable born during Testnet beta-testing may end up on Matic Mainnet some day.

## What's in my name for you? (Что в имени тебе моём?..)
- Temporary URI pointer that only you can change later, that survives urix.me website (OpenSource) in case of any service disruption
- Keys, or names, can mean NFT on another blockchain, with ownership verified in decentralised trustless manner (think oracles...) so 2nd level systems for Ethereum ERC721 are possible
- Name can mean a business idea, with royalties to the author, to our platform and to user-facing marketplace from each sale
- Name can be a world encyclopedia article
- **Bodyhash** is one of the possible fields and is used if you want to make certain content of HTTP (or other protocol) response body provable later
- **Merkleroot** is used when you want crypto-provability of a small part of structured content to a smart contract (no idea yet what for, but nice feature nevertheless)
- Merkleroot is used when you want to prove a paragraph from a certain document as part of body content to a person, but without revealing the entire document folder (useful for displaying and proving to the public something, if you are under NDA for the rest, just as one example)

## What other fields URIX token may have?
- **Tags**: an array of links to other URIX tokens representing a hierarchy of topics
- **Parents**: an array of links to parent notions. Examples: several scientific ideas giving birth to a new invention; a franchisee representing his business with a link to the franchise; an Ethereum cryptokitty with it's parents recorded on our 2nd level blockchain.

## What's a Slug?
This term comes from URL shorteners, and inititally URIX was just an URL shortener (decentralised) service.

There are URIXes with a custom slug and without. Every URIX has index, or ordinal: the number, starting with 0, which increments when a new token is minted. Some URIXes also have a string, stored as **slug** field in token's blockchain metadata.

So slug is token's name/key representation. Without custom slug, you can address a token in three ways:
- By decimal representation of it's index, e.g. urix.me/0 (genesis URIX)
- By hexadecimal representation of it's index, e.g. urix.me/0xFF
- By Base64 MIME representation, with one exclusion: we have to replace slash / with e.g. underscore, as it has a special meaning in our syntax; maybe + is also worth replacing to avoid confusion with space (' ') urlencode. E.g. urix.me/b/YW5k_yBt for a number if 48 bits (6 bytes) are enough for it's binary representation

With a custom slug _my-slug_, you can just go to urix.me/my-slug. But you can also address it in ways listed above.

A token can be minted with a custom slug, if there was no such slug in the existing ones. When mass-minting by a single call to a function, it's worth first check availability of custom slugs by calling a free, read-only function first.

In the minting process, URIXes with already taken slugs will just get ordinal indices. A slug cannot be changed afterwards, but you can mint another token, providing the previous one as it's parent. URIX minted without a custom slug, cannot gain it later.

Any string can be a custom slug if it doesn't contain #, ? and (possibly) other URI-inconvenient characters. It has to be not one of the following:
1. string consisting of only r[0..9] - as that would mean a decimal representation of token index, e.g. urix.me/666
2. string consisting of only r[0..9a..f]/i prepended by 0x - a that would mean a hexadecimal same, e.g. urix.me/0xABC0
Every token can be addressed as decimal, hexadecimal, base64 or (when present) it's custom slug.

If it contains /, then it becomes a leaf in the tree of notions. However, it has to be addressed with a prefix: urix.me/p/path/to/tree/leaf/example, p meaning "path".

This is done so that we reserve first-level (root) notions for ourselves, or for our affiliates (example: urix.me/cat/0x&lt;genetic_code&gt; may mean a CryptoKitty later)

So if a Chinese girl named Ying wants to reserve a name for her kitty named Tom, she can provide ying/cats/tom as the slug, but the URIX will be: urix.me/p/Ying/cats/Tom

We will also reserve small numbers (<1000 decimal) and all custom slugs that contain less than 3 symbols. So, alas, that baby urix.me/666 is ours. And any number of initial names, that we deem interesting.
Like name urix itself.
