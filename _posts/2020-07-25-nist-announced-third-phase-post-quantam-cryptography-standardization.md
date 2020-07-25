---
title: NIST has announced the beginning of the third phase of post quantum cryptography standardization
layout: post
image: https://live.staticflickr.com/2175/2028118171_4e33f12da7_k_d.jpg
---

NIST recently announced on its website the [launch of the third phase of post quantum cryptography standardization](https://csrc.nist.gov/News/2020/pqc-third-round-candidate-announcement). The third phase included 3 candidates for digital signature and 4 candidates for asymmetric encryption. Also 8 alternative candidates were presented. I thought that Khabrovchan would be interested in this event. More details under the cat.

## A bit of history.

The idea of quantum computing was first proposed in the early 1980s to model complex quantum mechanical systems. Soon it turned out that quantum computing can give a huge acceleration for solving other problems, such as number factorization and discrete logarithmization in a group of points of an elliptic curve.

This has become an essential problem for cryptography, as the safety of common standardized systems depends on the complexity of solving these problems.

Nevertheless, quantum computing remained only a beautiful abstraction for quite a long time, which was not technically feasible to implement. But recently the possibility of creating quantum computers has been revised and this has encouraged NIST to launch an open competition in 2016 for the creation of new post quantum standards. More precisely, NIST is interested in creating new standards for asymmetric encryption (Public-Key Encryption) and digital signatures.

There are 69 teams from all over the world who have applied for the competition. The topic was widely covered and there were even posts on the Habra. Only 26 out of the proposed schemes were submitted for the second stage. And so, on July 22, 2020, the finalists of the second stage were announced, which went on. Only 4 candidates for asymmetric encryption and 3 candidates for digital signature were left.

## Candidates who passed to the third stage

So, candidates for the new postquantum digital signature standard:

CRYSTALS-DILITHIUM - Is a representative of cryptography on grids. It's based on the intermittent Fiat-Shamir scheme. Cryptanalysis is reduced to solving Module-LWE and Module-SIS problems. Has good productivity and can be effectively realized on low resource devices. NIST asked the authors to add a set of system-wide parameters for Level 5 security.

FALCON - Also a representative of cryptography on grids. But it is based on the GPV framework. Cryptanalysis is reduced to the task of SIS on NTRU grids. The main disadvantage of this scheme is a complex software and hardware implementation. The scheme uses calculations over floating point numbers, which greatly complicates both the analysis of resistance to attacks through third-party channels, and makes difficult to implement for low-resource devices.

Rainbow - Is a precursor of cryptography on multi-variant transformations. It is based on the UOV scheme. The main advantage is the size of the digital signature. But because of the large size of the key this scheme is recommended to use only for specific tasks where the size of the keys is not critical.

NIST also stated that at least one of the schemes CRYSTALS-DILITHIUM and FALCON will be standardized. Thus, cryptographic lattice-based schemes are likely to be used for digital signatures in the future. And for more specific Rainbow tasks.

For asymmetric encryption, we've moved into phase three:

**Classic McEliece** - Is a representative of cryptography on error correction codes. The basic design of the scheme was proposed back in 1979 and is well researched. It has small ciphertext sizes, but a very large key size. Because of this, it has the same problems as the Rainbow and is recommended to be used only for specific tasks.

**CRYSTALS-KYBER** - Is a representative of cryptography on grids. Cryptanalysis comes down to solving a Module-LWE problem. To provide resistance to attacks with adaptively matched ciphertext, the Fujisaki Okamoto transform is used. Has good performance and security, but NIST also remind that Module-LWE is a relatively poorly researched problem and requires more detailed cryptanalysis.

**NTRU** - Is a representative of lattice cryptography. It is based on the NTRUEncryt scheme, which was proposed over 20 years ago. The NTRU problem, unlike Module-LWE (and other modifications), has been studied very well, which is a very important factor.

**SABER** - Is a representative of cryptography on grids. Cryptanalysis comes down to the MLWR (Module-LWE) problem, where instead of adding it to the error vector it uses 
rounding off to a smaller module). The Fujisaki-Okamoto conversion is used, as in CRYSTALS-KYBER. 

In general, the situation is similar - for general use, lattice-based schemes are recommended. But NIST made the observation that only one of the lattice-based schemes (CRYSTALS-KYBER, NTRU, SABER) will be standardized.


### Alternative circuits.

NIST also selected 8 alternative schemes that were not included in the final, but are promising.


Among the digital signature schemes:


SPHINCS+ and Picnic are schemes based on symmetric cryptoprimitives. Cryptanalysis of SPHINCS+ comes down to the persistence of hash functions, while Picnic comes down to NIZK and block ciphers. These schemes are quite new and poorly researched. But their main drawback is still their huge signature size, which makes them inapplicable for many tasks.
GeMSS - Similar to Rainbow, but based on HFE instead of UOV. It has a larger key size and a slower signature process. Selected as an alternative in case the Rainbow is vulnerable.

Among the asymmetric encryption:


- BIKE - Is a schema on error correction codes. Requires a more detailed security investigation.
- FrodoKEM - Is a representative of cryptography on grids. Cryptanalysis comes down to the LWE problem, which is more studied than Module-LWE (and other varieties). It has too slow algorithms шифрования\расшифрования.
- HQC - Is a scheme on error correction codes. It is based on quasi-cyclic codes. Has too slow algorithms шифрования\расшифрования.
- NTRU Prime - Is a representative of cryptography on grids. It has good protection against algebraic attacks.
- SIKE - Is the only scheme (among those submitted to the contest) that is based on elliptic curvature curves. Requires more detailed study. 

## Summary

Over the past four years, NIST has analyzed proposed postquantum schemes from around the world. Among the proposed schemes, the dominating position is occupied by the schemes on the grids. But they (as well as other directions) require more detailed study. NIST plans to conduct a detailed analysis of the remaining candidates within the next 3 years. 

It should be noted that there are already standardized diagrams on grids in the world: one, two. So, most likely, it is cryptography on the grids that will be increasingly replacing the usual RSA and ECDSA in the coming years. But at the same time, other solutions will be popular in highly specialized areas.
