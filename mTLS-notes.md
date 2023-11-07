# How is mTLS different from what was described in lectures

## How does TLS work:

**Symmetric cryptography** encrypts and decrypts data with a secret key known to both sender and receiver, there can be issues with establishing a secure key.

**Asymmetric cryptography** uses two keys, a public[^1], and a private key, these keys are related by a problem believe to be hard to reverse:
- In RSA the hardness comes from the fact that it is hard to factor large numbers
- Many modern crytography methods use arithmetic on elliptic curves points (Rc: ECDLP)
And so even though the keys are related, given the public key it is (for no) unfeasible to calculate the private key. This faciliates encryption using the public key that everyone has access to, but decryption using only the private key.

This increased practicality does come at a cost: much larger keys are used, (it is unfeasible to calculate the private key from the public key) and so this method is thousands of times more computationally intensive, and therefore slow. [^2]

To overcome this TLS uses asymmetric curve cryptography to share a **session key**, this will be used in future messages that are encrypted using symmetric cryptography.[^3]

## mTLS - Mutal TLS

As the name suggests, this method of security relies on mutual authentication - specifically, both parties need to prove they have the correct private key.

The easiest way to prove that you have a private key is to decrypt a message encrypted with the corresponding public key.

## The difference

mTLS has additional steps when compared to TLS, see below:

1. Client connects to server
2. Server presents its TLS certificate
3. Client verifies this certifcate
4. **Extra Steps**
5. Client and server exchange messaged over the encrypted connection

These extra steps are:

1. Client presents its TLS certificate
2. Server verifies this certificate
3. Server grants access

This *"TLS certificate"* step sounds slightly different to what was described above though! That is because this certificate contains information used to verify the senders identity, such as the public key, who issues the certificate, when it expires, etc. This step and the one following encapsulates the whole process of proving you own a private key (there is more to it than just decrypting a signed message, but thats the essential part).
  

# Where is mTLS frequently used

# Example application that uses mTLS

# Diagram to show the process


### References

https://www.internetsociety.org/deploy360/tls/basics/
https://www.cloudflare.com/en-gb/learning/access-management/what-is-mutual-tls/


[^1]: Hence why this is also called public-key cryptography
[^2]: Can think of extra key length being used in maintaining the relationship between the public and private keys, what's left over is used in the encryption. E.g. a 2048-bit asym key is approx equal in security to a 112-bit symm key. 
[^3]: And to prove that a website owns its public key, certificate are used.
