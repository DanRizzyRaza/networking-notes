# How is mTLS different from what was described in lectures

## How does TLS work:

**Symmetric cryptography** encrypts and decrypts data with a secret key known to both sender and receiver, there can be issues with establishing a secure key.

**Asymmetric cryptography** uses two keys, a public[^1], and a private key, these keys are related by a problem believe to be hard to reverse:
- In RSA the hardness comes from the fact that it is hard to factor large numbers
- Many modern crytography methods use arithmetic on elliptic curves points (Rc: ECDLP)
And so even though the keys are related, given the public key it is (for no) unfeasible to calculate the private key. This faciliates encryption using the public key that everyone has access to, but decryption using only the private key.

This increased practicality does come at a cost: much larger keys are used, (it is unfeasible to calculate the private key from the public key) and so this method is thousands of times more computationally intensive, and therefore slow. [^2]

  

# Where is mTLS frequently used

# Example application that uses mTLS

# Diagram to show the process


### References

https://www.internetsociety.org/deploy360/tls/basics/


[^1]: Hence why this is also called public-key cryptography
[^2]: Can think of extra key length being used in maintaining the relationship between the public and private keys, what's left over is used in the encryption. E.g. a 2048-bit asym key is approx equal in security to a 112-bit symm key. 
