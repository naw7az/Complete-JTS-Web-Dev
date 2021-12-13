# Section: SSH(Secure SHell)

**There are 3 techniques used in SSH :**
Encription is a way to hide/jumble a piece of text which is impossible to read by a third party and a person need to decrypt it before reading.

1. Symmetrical Encryption
Uses 1 secret key for both encrytion(E) and decrytion(D).The secret key is exchanged between client and host using key exchange algorithm. The key is generated for each of the SSH session.

"Hello" -> Key112(E) -> "E11-32ds" -> Key112(D) -> "Hello"

2. Asymmetrical Encription
Uses two separate keys for encryption and decryption.
The client and host uses a pair of keys(public and private).
the public key (can only)encrytps the data and only the private key that is linked to the public key can decrytp that data.

Say, A has **pubA** and **priA** as two keys. B has **pubB** and **priB** as two keys. B will share **pubB** to A and A will send the data, **pubB** will encryt it and to decryt the data B will use **priB** and vice versa.

      PubA(encrytps)                             PubB(encrytps)
      A                                          B   
      PriA(decrytps pubA encrytion)              PriB(decrytps pubB encrytion)

3. Hashing
Hasing is a way where the client and host uses the key data to encrytps (**HMAC-Hash Message Authentication Code**). Used it in tazapay api call. the client send data along with the hash and the host uses HMAC the encrypt the client data and key to check whether it matches with the hash client has sent. This is used to check whether the data got changed in between the exchange.
