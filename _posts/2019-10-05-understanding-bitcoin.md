---
layout:     post
title:      Cryptocurrency explained
date:       2019-10-05 12:31:19
summary:    Understanding why were cryptocurrencies created and how bitcoin works. 
categories: blockchain
---


<!-- # cryptocurrency explained.  -->

Over the past few days I have been going through various blogs, research papers, youtube videos, books to read and gain knowledge about Cryptocurrency, which has been a pretty talked about topic recently. Unless you have been living under a rock, it is highly unlikely that you have never heard of _(bitcoin, blockchain, ethereum, mining)_ before. Through this post, I will try to explain how these technologies/currencies work and why were they created, and how can they change the way we do transactions now. 

To understand this Digital Currency, let us understand, how currency works and has been working so far. 
Initially, we had [barter](https://en.wikipedia.org/wiki/Barter) system, which was replaced by money mainly because exchange is not always convenient and efficient. 
Due to this, currency started to mint. The exchange problems were solved and this system was largely based on trust. The kings used to have their [royal seal](https://en.wikipedia.org/wiki/Alyattes_of_Lydia) on the coin signifying that this currency is valid. However forgery was very common as making a coin and copying the seal was not that a difficult task, but still way much better than Barter. 
With time, the gold coins transformed into paper money, which was widely circulated across the world by [explorers](https://en.wikisource.org/wiki/The_Travels_of_Marco_Polo/Book_2/Chapter_24). Trade flourished across countries through this paper money, and exchange of currency started around that time too, and by around 1860, Western Union, spearheaded e-money with electronic func transfer via telegram. With time cards came, and with the rise of internet the e-money started to boom. 
The reason, why I am focussing on the history of currency, is because I want you to understand what is common between all these systems of currency. From exchanging coins with royal seals, to exchanging paper currency, with issuance from bank/government, to starting e-money (banks giving cards). If you try to find the pattern, you will see that all of these currencies are **Centralized**.

By centralized, what I mean is that everytime there is an authority that is responsible for issuing the currency. Someone who says that, Yes, I am accountable for this currency and this currency is valid. Be it a king, who imprints the coin with its royal seal, or the government. The transactions have always been based on **Trust**. If I pay ₹100 to X, the bank issuing the currency is responsible to pay that ₹100 to X. Hence the currency so far being used is based on Trust, and is Centralized. Due to this we are always bound to law, cannot be innovative and creative with our money, always under control and at a risk of interference. Also, the banks would charge some amount for transactions as _transaction fee_. The point to be noted is that, crypto currency is not flawless, so it just provides as an alternative currency as of now. Due to all this, a currency was needed which was not based on trust, and is not centralized. 
> `Cryptocurrency is a decentralized trustless verification system + Math.`

Now, one thing I would like to mention here is that just like normal currency, you need not know how cryptocurrency is made or how it works to use it. Diving into the technical details, let us understand everything with an example.

Say there are 4 friends _A, B, C and D_ who hang out pretty often, and hence they need a system to keep track of money. What they do is, they keep a ledger and add all the transactions in it, and at the end of the month they settle it.

```
  * ledger *
A spends ₹1000
B spends ₹2000
A spends ₹500
C spends ₹300
A got ₹200 from D
```
So at the end of the month they will have 
```
  * ledger *
A spent ₹1300
B spent ₹2000
C spent ₹300
D spent ₹0

```
and then they will settle up and pay to the respective person. The thing is that the ledger is accessible to all four of them, and they all can edit i.e and add or delete transactions. This method is not correct, as it has very high chances of fraud. D might just say that he spent ₹10000, without it being verified by others. This can be prevented by the party editing the ledger to sign it, i.e add a Digital Signature, but again a signature can be easily copied and hence forgery is easy. Hence, we need a system that ensures that the correct person is editing the ledger.
To prevent forging, everyone generates a Secret Key `sk`, and a Public Key `pk` pair. Now the signature is mainly a function say `sign(message, sk) -> signature` which generates a hash, and there is a function say `verify(messgae, signature, pk)` which gives out a value True or False. The function `sign(message, sk)` is a cryptographic hash function. The thing about a cryptographic hash function is that they are irreversible. It is practically impossible to determine what could have caused the hash and no matter how big or small the message, is, the hash generated will be of a fixed length.  Instead of hit and trial, one cannot cause the same hash, and hence, it is practically impossible as the hash used is very large _(SHA-256 -> 2<sup> 256 </sup> combinations)(will be talking about this in a bit.)_ The function verify, means to verify is the transaction is not fraudulent. It also see;s that all the transactions balance. 
> The ledger is the currency. 

The problem with this solution is that the fate of the entire money system depends on the company running the mint, with every transaction having to go through them, just like a bank. We need a way for the payee to know that the previous owners did not sign any earlier transactions.

One thing which you might have noticed, is that this system of ledger that I just explained is centralized as well, which I had focussed on earlier. We have found a way to secure the transactions but there is only one ledger, and everyone is making transactions in their own ledger. As I had mentioned earlier, the cryptocurrency is decentralized. To make this currency decentralized, we will give one copy of the ledger to all four friends (A B C and D). Now this ledger becomes a decentralized currency.

So now, all have personal copies of the ledger, and now adding the transaction has become a different process. Like they can still add the transaction in their personal ledger, but it wont match with the ledger of someone else. Say, B adds `B spent ₹5000` to his ledger, but that information wont be added on the ledger of A or C or D. To have all the ledgers on the same track, one must broadcast their ledger so that everyone in the network updates their ledgers with the most recent transactions. So, B would update its ledger, and then broadcast his ledger so that everyone verifies the transaction and update their ledgers as well. Hence through this example, we have made a trustless decentralized verification system. 
But with so many ledgers being broadcasted constantly, which ledger is to be trusted? This problem has been address in the original [Bitcoin Paper](https://bitcoin.org/bitcoin.pdf). 

The bitcoin paper mainly said to trust the block/ledger with the most computational work being done(proof of work). To understand this, let me quickly tell you what a blockchain is. In this case, we can understand every block to be a ledger, and every block has a header with the hash of the previous block. Hence making a chain. This chain of ledgers is called a blockchain. We cannot reverse two blocks as that will require to change the complete chain that lies ahead of us. Hence it cannot be chainged without redoing the proof of work.

![](/images/bitcoin1.png) 


To understand the proof of work, one must understand the concept of Cryptographic Hash Functions. I did tell earlier that crypto hash functions are irreversible. One of the example of a crypto hash function is SHA-256, which generates a 256 bit long string for any input and even the slightest change in the input can change the complete hash. The thing to be noted is that SHA256 will output 256 digits, no matter how long or short the input is. It is practically impossible to reverse engineer the algorithm, but feel free to try. You can see the SHA-256 algorithm in action [here](https://emn178.github.io/online-tools/sha256.html).
The proof of work involves scanning for a value that when hashed, such as with SHA-256 the hash begins with a number of `n zero bits`. 
For our network, we implement the proof of work by incrementing a nonce in the block until a value is found that gives the blocks hash the required zero bits. Finding this number is called *mining*, and the people who do this are called *miners*. The paper also said to trust that chain with the most number of nodes, hence while updating their ledger, they also keep track of all other chains, and then eliminate the smaller chains as miners start working on the longest chain. 
Proof-of-work is essentially one-CPU-one-vote. The majority decision is represented by the longest chain, which has the greatest proof-of-work effort invested in it. If a majority of CPU power is controlled by honest nodes, the honest chain will grow the fastest and outpace any competing chains. To modify a past block, an attacker would have to redo the proof-of-work of the block and all blocks after it and then catch up with and surpass the work of the honest nodes the number of zeros vary a lot. What the miner gets in return is a block reward. With every block added to the network, the total amount of money increases in the economy, as there is no one issuing the block reward. Hence through this proof of work, it is nearly impossible to create fraudulent transactions. This miniature lottery is such that there is one winner every 10 minutes (in case of  bitcoin). This time may change for other cryptocurrencies.  

We can understand the whole network through these steps


The steps to run the network are as follows:

1. New transactions are broadcast to all nodes.
2. Each node collects new transactions into a block.
3. Each node works on finding a difficult proof-of-work for its block.
4. When a node finds a proof-of-work, it broadcasts the block to all nodes.
5. Nodes accept the block only if all transactions in it are valid and not already spent.
6. Nodes express their acceptance of the block by working on creating the next block in the chain, using the hash of the accepted block as the previous hash. Nodes always consider the longest chain to be the correct one and will keep working on extending it. If two nodes broadcast different versions of the next block simultaneously, some nodes may receive one or the other first. In that case, they work on the first one they received, but save the other branch in case it becomes longer. The tie will be broken when the next proof of work is found and one branch becomes longer; the nodes that were working on the other branch will then switch to the longer one.



I hope through this blog, I have been able to explain what cryptocurrencies are and how they are different from the currencies that we are using right now. This all is based on my understanding, and do let me know if I went wrong somewhere, I will appreciate it. Also, feel free to comment your doubts and suggestions. 


