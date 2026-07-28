---
schema_version: "1.0.0"
document_id: "dd229faa8783771c442511e996d6f2dab093fe2ec136ebcac9345afa8d295e77"
company_key: "btq-technologies-corp-common-stock"
company: "BTQ Technologies Corp. Common Stock"
source_id: "btq-technologies-corp-common-stock-news-import-4b4199d8e235"
canonical_url: "https://www.btq.tech/blog/whats-the-difference-between-todays-cryptography-and-post-quantum-cryptography"
published_at: "2023-09-07T00:00:00+00:00"
first_seen_at: "2026-07-21T11:47:25.232763+00:00"
fetched_at: "2026-07-28T21:33:41.699737+00:00"
content_hash: "sha256:1861c66ac7a9d68de415110793df069bef02d0265c102861e03754cebb12511d"
---

# What’s the Difference Between Today’s Cryptography and Post-Quantum Cryptography?

Cryptography, or the study of securing our data, is the only reason our digital world expanded as it did. We use cryptographic algorithms to keep our data safe when we are online. But here's the catch - the rise of quantum computing could shake things up and completely destroy online security. Luckily, there’s a solution on the horizon. Post-quantum cryptography (PQC) is the next-gen security scheme built to stand firm against even the most powerful quantum computers. Though today's cryptography and post-quantum cryptography are very different, the research and innovation to secure against the quantum threat is ongoing to stand up against the quantum threat.


## The Current Landscape of Cryptography: At Risk


In the simplest terms, cryptography is the practice of securing communication. It's the backbone that makes our digital world secure and trustworthy. But how exactly does it work?


RSA and Elliptic Curve Cryptography (ECC) are two of the most popular asymmetric cryptographic algorithms. They secure a significant part of the world's digital security infrastructure, from secure web browsing to secure email and shell remote access.


Most modern cryptographic systems are built upon the difficulty of solving certain mathematical problems. These are problems that are easy for a computer to do in one direction but difficult to reverse. An excellent analogy for this is the process of baking. It's straightforward to bake a cake using the recipe and ingredients but try deconstructing that cake back into eggs, flour, and sugar. It’s almost impossible, right? This idea forms the concept of["trapdoor functions."](https://en.wikipedia.org/wiki/Trapdoor_function?ref=btq-publication.ghost.io)


​​The RSA algorithm, named after its creators Rivest, Shamir, and Adleman, was first introduced to the world in 1977 and used this concept of a “trapdoor function”. Multiplying two large prime numbers is easy, but it's computationally difficult to factor a large number into two primes. This created a practical and secure cryptographic system since breaking a 2048-bit RSA key (a prime number with 617 decimal digits) would take 1 billion years with a classical computer.


In 1985 Elliptic Curve Cryptography (ECC) arrived, introduced by mathematicians Neal Koblitz and Victor Miller. ECC was a massive leap in efficiency and security over RSA. The security of ECC is based on the elliptic curve discrete logarithm problem. For the same level of security, ECC keys are much shorter than their RSA counterparts, making them faster and less computationally intensive. This is especially useful in mobile devices and the Internet of Things.


RSA and ECC are examples of asymmetric cryptography algorithms, also known as public key cryptography. Unlike symmetric cryptography, like AES, which uses the same key for both encryption and decryption, asymmetric cryptography involves a pair of keys: a public key for encryption and a private key for decryption.


Here's how it works: if person A wants to send a secure message to person B, they would encrypt the message with B's public key – accessible to anyone. Only person B, who holds the corresponding private key, can decrypt the message. Anyone else who intercepts the message wouldn't be able to decrypt it because they don't have access to person B's private key. This ensures the secrecy of communication. Someone could also use a private key to sign a document, message, or transaction, providing proof of origin and integrity. Anyone can verify the signature using the corresponding public key, but they can't forge it without access to the private key. This is critical for life on the internet, including for email, software updates, electronic voting, and blockchain transactions.


These two cryptosystems secure large parts of the internet. When platforms encrypted with these two systems are hacked, it’s not due to the vulnerability of the RSA and ECC algorithms themselves but a bug in the implementation, supporting code, or through phishing that reveals the private key. These algorithms have proven secure over decades of use.


But there’s a twist. This safety could be disrupted with the advent of quantum computing.


## Quantum Computing: A New Challenger Approaches


Quantum computers differ from classical computers by exploiting quantum mechanical phenomena of superposition and entanglement. Quantum bits, or 'qubits,' unlike classical bits that can either be 0 or 1, can exist in a probability of these states. When these qubits become entangled, a change to one qubit affects the other because their states depend on each other, regardless of distance. These principles allow for faster processing and higher computational power.


Shor's algorithm, when run on a sufficiently large quantum computer, could theoretically factor large numbers or compute elliptic curve discrete logarithms efficiently, breaking the safety of RSA and ECC and rendering it useless. In other words, the baked cake could now be feasibly turned back into its original ingredients!


Breaking a 2048-bit RSA key would take 1 billion years with a classical computer. A quantum computer could do it in 100 seconds. ECC is even more vulnerable to quantum computers, requiring even fewer qubits than breaking RSA encryption.


## Post-Quantum Cryptography: The Post-Quantum Era


What can we do to protect ourselves from this threat? This potential vulnerability leads us to post-quantum cryptography, a classic cryptographic method designed to be secure against an attack by a quantum computer. Post-quantum cryptography aims to prepare new cryptographic methods for the day when quantum computing becomes a reality.


Post-quantum cryptographic algorithms are based on mathematical problems that appear (based on current knowledge) to be resistant to quantum attacks. These include lattice-based cryptography, code-based cryptography, hash-based cryptography, and multivariate cryptography.


These mathematical problems and cryptographic methods being developed are not necessarily new. They didn't receive much attention because they weren't needed in a pre-quantum world because they were less efficient or more computationally intensive than the dominant RSA and ECC algorithms. However, the looming quantum threat to these standardized algorithms has caused a resurgence in their study and application.


Scientists and engineers are now developing encryption methods robust enough to withstand the computational prowess of quantum computers. The core idea is to find mathematical problems that are difficult for both classical and quantum computers for a higher level of security for the post-quantum future.


Let’s go through some of the most promising groups of post-quantum cryptographic algorithms:


### Lattice-Based Cryptography


Lattice-based cryptography is one of the most promising areas of post-quantum cryptography since they have been well-studied for decades. One of the central problems in lattice cryptography is the 'shortest vector problem.' Given a lattice and a starting point, the challenge is to find the nearest point in the lattice. That problem is computationally difficult for both classical and quantum computers in high-dimensional spaces. Even imagining 4 dimensions is hard for us mortal beings, let alone more!


### Code-Based Cryptography


Code-based cryptography originated in the 1970s with the development of the McEliece cryptosystem. This system was based on a problem in coding theory: the study of the properties of codes and their use for specific applications. For example, if you had a secret language only you and your friend understood or a crossword puzzle where the clues keep changing. The McEliece cryptosystem, specifically, relies on the difficulty of decoding a general linear code.


### Multivariate Cryptography


Multivariate cryptography is based on systems of multivariate polynomials. These are mathematical expressions involving several variables. Imagine a complicated recipe with loads of ingredients, and you must recreate a dish from a taste without knowing the ingredients or the amounts. This is a bit like multivariate cryptography. Instead of ingredients, though, it uses mathematical equations with many different parts (or variables).


### Hash-Based Cryptography


Hash-based signatures were one of the first practical methods proposed for post-quantum cryptography. They are based on cryptographic hash functions, which take an input (or 'message') and return a fixed-size string of bytes. This hashing process is easy, but finding the message corresponding to the output hash is difficult. This is the process on which Bitcoin mining is based, as well.


However, there are more fields of mathematical problems being developed. NIST announced the Post-Quantum Cryptography Standardization project, which involves academic and industry players in developing and evaluating new cryptographic systems. Four finalists were announced in 2022. However, it is now adding additional candidate algorithms since a few candidates in the lower stages of the competition have been cracked.


BTQ’s post-quantum cryptography scheme,[Preon](https://preon.btq.com/?ref=btq-publication.ghost.io) , was recently selected by NIST as a candidate for the Post-Quantum Cryptography Standard. Hear more about Preon in the BTQ podcast,[The Quantum State](https://www.youtube.com/watch?v=f-imiYz3wJg&ref=btq-publication.ghost.io) .


While no post-quantum method is perfect, and each comes with its own trade-offs, they are building a path toward a secure post-quantum world. As NIST works on standardizing post-quantum cryptographic algorithms, these areas represent the cutting edge of cryptographic research. It's an exciting time to be in the field of cryptography as researchers, practitioners, and institutions around the globe collaborate to design our digital world's quantum-proof future. Companies working on fundamental cryptographic research, collaborating with quantum scientists to test the robustness of algorithms, and creating infrastructure for security and crypto agility when quantum threat is here will be fundamental to the entire digital safety and infrastructure in the world.


‍
