# Running Quantum-Safe Applications on K8s

[ibm quantum](ibm.com/quantum)

runs on k8s, quantum safe

## Understand the risk

Imitation game ... the computer that Turing built had vacuum tubes. WRT Quantum computing, we're at that same stage.

Computing has limits. There are hard problems. Can you find polynomial time solutions to these hard problems? Not yet... 

A subset of these hard problems are easy for quantum computers to solve. 

Focusing on one in particular....

Shor's quantum algorithm (A quantum algorithm): Factoring extremely large numbers. Came up with constant time for large numbers. QFT -> Quantum F? Transforms are the key to that.

To run Shor's algorithm, you need large numbers of computers.

The alternative to shor's algorithm is exponential in terms of how long it takes to solve.

IBM is currently at 100 qubits. Microsoft is pushing in this area also. This puts te entire volume of encrypted data on the internet -- banking, gov't, etc -- at risk. The time horizon is decades, probably.

## Becoming Quantum Safe

Use algorithms that are resistant to attacks by both quantum and classical computers.

NIST has recommendations as to how to implement quantum safe cryptography, released as of this year.

[post quantum cryptography alliance](https://pqca.org) ... clearinghouse for post-quantum cryptography
- liboqs ... library of quantum safe algorithms
- openssl 3 provider ... integrates into openssl where many keys are generated
    - X.509 certs, etc.
    - TLS key exchange / authentication

## Protecting Applications

Journey to quantum safe:
- discover ... scan source and object code to locate usages of cryptography. Build a cryptography bill of materials. Where do we need to make changes? Inventory your cryptography.
- observe ... see it in actions to verify the easiest places to make subsitutions
- transform ... implement the quantum safe patterns in code

vectors:
 - clients
     - download some libraries, install, and ...
     - configure openssl!
 - public internet
     - enable PQC in WAFs
 - internal networks
     - configuration changes in istio/envoy

question: even if the client doesn't have quantum safe cryptography, there's nothing preventing industry from making their internal networks and k8s clusters quantum safe, right? Is decrypting in classic cryptography and re-encrypting in qs cryptography a thing?

## Next steps
- Learn
- Start inventorying your crypto

