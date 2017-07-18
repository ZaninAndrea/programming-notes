# Public communication
## Diffie-Hellman protocol
### Algorithm
Alice and Bob choose a large prime number $$p$$ and a number $$g$$ such that $$1\lt g \lt p$$, those are public.
Alice secretly chooses an integer $$n$$ and Bob secretly chooses an integer $$m$$
Now Alice sends Bob the number $$g^n\mod p$$ and Bob sends Alice $$g^m \mod p$$
Using her secret Alice computes $$s \equiv (g^m)^n\equiv g^{mn} \mod p$$
Using his secret Bob computes $$s \equiv (g^n)^m\equiv g^{mn} \mod p$$
Now Alice and Bob have a secret key $$s$$ known only to them, which can be used to send messages via any number of secure private-key cryptosystems. 

### Security
The security of the algorithm relies on the difficulty of computation of discete log problem, which is to compute $$m$$ and $$n$$ knowing $$p$$, $$g$$, $$g^n\mod p$$, $$g^m\mod p$$

There is no efficient algorithm to compute discrete logs and it's widely believed that there is no faster way to find $$g^{mn} \mod p$$ than computing the discrete log

### Choosing the parameters
- The prime $$p$$ should be chosen so that the largest prime factor of $$p=1$$ is large. Otherwise we are vulnerable to the Pohlig-Hellman algorithm, which is based on the Chinese Remainder Theorem
    - to avoid this $$p$$ is often chosed as $$p=2q+1$$ where q is a prime (called Sophie Germain prime)
- The base $$g$$ should be chose so that $$g$$ has a large order