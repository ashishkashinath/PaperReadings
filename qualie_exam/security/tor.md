#Tor : The Second Genration Onion Router

## Terms 

Perfect forward secrecy, Congestion Control, Directory Servers, Integrity Checking, Configurable Exit Policies.

###High-level ideas

Works on the real-world internet, requiring no special privileges or kernel modifications.

Tradeoff between : Anonymity, Usability & Efficiency.

### Need for Privacy & Anonymity

Researchers need it to deanonymize data -- cognitive bias.

Compnanies need to protect sensitive data; competitors given different product sheets

### What is anonymity,technically?

Naive: I didn't write my name on it,
No one can prove its me

Adversary/observer can't link participants to actions. [Fitzman & Hansen](freehaven.net/anonbib)

Say Alice is buying socks. And eve is observing it. Eve can tell Alice is doing something, (obsevavibility)()

* Eve can tell someone is buying socks.(not anonymity)

* Eve can't tell *alice* is buying socks. Either probabilistically or Mathematically or by Observing many instances)

*Unlinkability:* Say Alice is posting as Bob. Unlinkability is eve's inability to link Alice to a particular profile.

Humanity -- lot of issues can be solved by freedom of expression, communication, anonymity.

### Threat Model

Started with a usability (not adversary) requirement. This has to be useful for interactivity protocols on the webs.  


Forward Anonymity: Alice runs a relay or Alice uses a relay run by other users.

Watching the input link at the relay. Now can be deciphered.

Add encryption.

Tunneling through multiple relays -- no single p[arty can correlate the whole thing

**Design Point** What if eve watching input and output link? Yes, there is noise due to encryption, network latency etc. but it is still kB in, kB out. *Volume and timing information* can help eve correlate. Choumi and DCNets, MixNets.

Batch, reorder and transmit at a later point in time.


###User base requirement
Anonymity loves company -- unless there is large userbase, there is no anonymity.

Shared public system rather than a private system. UIUC legal investigating companies giving fake UIUC diplomas.

Minimize probability that happends over time

###Message Passing

Give each relays a public key: K1, K2, K3.

K3 then K2, then K1.

PKI is expensive, so not used for bulk traffic.

Alice negotiate a key with each server. associated with a circuit.

Circuit is a path though the network.

That's *Onion Routing in 90's.*

Integrity checking node by node or end-to-end.

###So

Alice first makes a TLS link to R1. R1 say already has a TLS link to R2.

one-way authenticated, one way anonymous NTor -- both have proofs.

create cell, 
pick a circuit ID
relay says created.
R1 and Alice share a symmetric key called S
They have it stored as S.circuti_id

Alice then says relay extend with first half of handshake -- encrypted with R2's public key. R2 then gets it, and picks a circuit ID.

Now Alice is told about it.

R2 then does connect to Bob.

###Protocols

Can we do it in IP? Need an IP nomalization layer. Anything less than a full IP doesn't work.

Take contents of TCP streams and send it across.













