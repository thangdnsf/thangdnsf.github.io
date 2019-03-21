---
layout: post
category: "Project"
title:  "Generate large prime numbers for RSA encryption algorithm"
tags: [Prime-numbers,Large-prime,Prime-generator]
sum: "This paper describes and implements the classical method to generate random strong primes used in cryptography. Specifically, the Rabin-Miller and Gordon algorithmsare presented in detail."
feature-image: "/resources/img/strong-prime.png"
---
### Overview

This paper describes and implements the classical method to generate random strong primes used in cryptography. Specifically, the Rabin-Miller and Gordon algorithmsare presented in detail.

<object data="/resources/prime.pdf" type="application/pdf" width="700px" height="700px">
    <embed src="/resources/prime.pdf">
        <p>This browser does not support PDFs. Please download the PDF to view it: <a href="/resources/prime.pdf">Download PDF</a>.</p>
    </embed>
</object>

<object data="/resources/primgen.pdf" type="application/pdf" width="700px" height="700px">
    <embed src="/resources/primgen.pdf">
        <p>This browser does not support PDFs. Please download the PDF to view it: <a href="/resources/primgen.pdf">Download PDF</a>.</p>
    </embed>
</object>

##### Github: [PrGlib](https://github.com/thangdnsf/PrGlib)

#GENERATE STRONG PRIMES FOR RSA 

_thangdn.tlu@outlook.com_

_ThangLong University_


#### I. GENERATION OF STRONG PRIMES

**_According to primes number, the average distance of two large prime numbers (n bit) is  n * ln2. And We prove the existence of primes in this distance._**

##### **1. Generate random integers**

We need to generate large random integer about 3072bit. Due to use in cryptography so a good random integer if it satisfies the following condition: it's a large integer. the values between numbers have to far apart.

In this PrGlib library, it was used RandomBits (NTL library) to goal generate random integers.

##### **2. PRETREATMENT**

We'll consider 2*n*ln2 numbers [n,n+2*n*ln) by Rabin-miller Algorithm. But we can improve this algorithm as follows:

>* Generate a list 1000 the first prime numbers.

>* Generate a array S with size = 2*n*ln2. default is zero

>* Let r=n%p (p is 1000 the first primes). And compute S[p*k-r]=1

we prove n+i always be divisible for p if S[i]=1.

After finish, we just consider n+i if S[i]=0.

so this improve algorithm, it eliminates more than 93% composite.

##### **3. CHECK FERMAT PSEUDOPRIME TO BASE 2**

##### **4. RABIN-MILLER- TEST**

we'll check 64 numbers, include of 20 the first primes and 44 random numbers.

##### **5. GORDON'S ALGORITHM FOR FINDING STRONG PRIMES**

Gordon's algorithm is as follows:

> 1. Find p-- and p+ as large random primes.
> 2. Compute p- as the least prime of the form p-=a--*p-- +1, for some integer a--.
> 3. Let po=((p+)^(p- -1)- (p-)^(p+ -1))mod (p-*p+).
> 4. Compute p as the least prime of the from p=po+a*p-*p+, for some integer a

##### **6. RUNTIME OF ALGORITHM**

OS: ubuntu

Language program C++

Use library: NTL and GMP

=> Generate prime numbers: 0→ 2s.

=> Generate strong prime numbers: 1→ 3s.

#### II. RSA ALGORITHM

##### **1. GENERATE KEY**

> Generate p and q as strong primes about 3072bit.

> Compute n=p*q and phi(n)=(p-1)*(q-1)

> Choose e, such as gcd(e,phi(n))=1.

> Let e*d=1 mod phi(n).

> Private key (n,d) Public key (n,e)

##### **2. ENCRYPT**

we'll encrypt a KEY{128,192,256}. 

Generate a array bits with size = 2048. And use 16 headbit and KEY{128,192,256}, so we have to random 2032-KEY.

Encrypt array bits:  C=M^e mod n

we should store C format base64.

##### **3. DECRYPT**

Decryption process do the opposite encryption with M = C ^ d mode n

#### References

[1]. _Are `Strong' Primes Needed for RSA?_,Ronald L. Rivest #,Robert D. Silverman y
November 22, 1999

[2]. _Strong primes are easy to find_, John Gordon, Cybermation L t d