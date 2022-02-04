# NFT Metadata

Our **Meta Z Items** are NFTs, meaning they would need metadata in order to be able to use them on the game. The metadata is a JSON document that contains:

* Item name
* Item GameID
* An image for item preview
* Data about 3D models that make up the item

Uploading images and large data to the blockchain is very expensive since they are large in size. The best practice is to only upload the link of the image to the blockchain and store the actual image on a server.

With an HTTP address like `https://example.com/my-nft.jpeg`, anyone can fetch the contents of `my-nft.jpeg`, as long as the owner of the server pays their bills. However, there's no way to guarantee that the _contents_ of `my-nft.jpeg` are the same as they were when the NFT was created. The server owner can easily replace `my-nft.jpeg` with something completely different at any time, causing the NFT to change its meaning.

This problem was demonstrated by an artist who [_pulled the rug_](https://cointelegraph.com/news/opensea-collector-pulls-the-rug-on-nfts-to-highlight-arbitrary-value) __ on NFTs he created by changing their images after they were minted and sold to others.

A protocol called **IPFS** (InterPlanetary File System) would work great to solve this problem.&#x20;

The InterPlanetary File System is a protocol and peer-to-peer network for storing and sharing data in a distributed file system. IPFS uses [content addressing](https://docs.ipfs.io/concepts/content-addressing/) to uniquely identify each file in a global namespace connecting all computing devices.

{% embed url="https://www.youtube.com/watch?v=5Uj6uR3fp-U" %}
IPFS Simply Explained
{% endembed %}

Adding data to IPFS produces a content identifier (CID) that's directly derived from the data itself and links to the data in the IPFS network. Because a CID can only _ever_ refer to one piece of content, we know that nobody can replace or alter the content without breaking the link.

Using the CID, anyone can fetch a copy of the data from the IPFS network as long as at least one copy exists on the network, even if the original provider has disappeared. This makes CIDs perfect for NFT storage. All we need to do is put the CID into an `ipfs://` URI like `ipfs://bafybeidlkqhddsjrdue7y3dy27pu5d7ydyemcls4z24szlyik3we7vqvam/nft-image.png`, and we have an immutable link from the blockchain to the data for our token.

