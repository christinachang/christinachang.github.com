---
layout: post
title: "Pass the Salt! Securing Passwords with Salting and Hashing"
date: 2013-05-28 20:07
comments: true
categories: 
---

If your application requires users to log in with their passwords and you are storing these passwords in a database, it's important that you protect your users' passwords in case of any security breaches. 

First rule: passwords should never be stored in the database unencrypted (in plain text).

The best method to protect passwords is to employ salted password hashing.

Hashing is an algorithmic function that turns data into a fixed-length fingerprint that cannot be reversed. The advantage of hashing is that if the input changes by even one character, the resulting hash is completely different.

<b>Example:</b><br>
<img src="/images/hash.png"></img>

After a password has been hashed, the hash is stored in the database. When the user logs in, the hash of the password they entered is verified against the hash of the password in the database. If the hashes match then the user is granted access.

Hashing a password, however, still does not provide adequate protection. It's possible to crack hashes by guessing at passwords, hashing those guesses, and then checking if the guess hashes are equal to the hashed password. These guess methods are commonly called dictionary attacks and brute-force attacks.

A dictionary attack uses a list of words, phrases, and common passwords that are hashed and then compared to the password hash. A brute force attack tries every possible combination of characters up to a certain length.

These attack methods work because every password is hashed the exact same way. Users with the same password would have the same password hashes. To prevent these attacks from successfully gaining access to user passwords, the hashes should be randomized by either appending or prepending a random string called a salt to the password before it is hashed.

<b>Example:</b>
<img src="/images/salted_hash.png"></img>

Salting turns the same password into a completely different hash each time. In order to verify that the password a user enters is correct, the salt needs to be stored in the database along with the hash. It's important that the same salt is NOT used for each hash. A salt should be random and not too short in length. When a user creates an account or changes their password, a new random should be generated.

<ul>Resources:
<li><a href="http://en.wikipedia.org/wiki/Salt_(cryptography)">http://en.wikipedia.org/wiki/Salt_(cryptography)</a></li>
<li><a href="https://en.wikipedia.org/wiki/Cryptographic_hash_function">https://en.wikipedia.org/wiki/Cryptographic_hash_function</a></li>
<li><a href="http://crackstation.net/hashing-security.htm">http://crackstation.net/hashing-security.htm</a></li>
</ul>