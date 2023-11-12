# PHP

---

### 1. Creating  openssl  initialization vector:

```php
    bin2hex(
        openssl_random_pseudo_bytes(
            openssl_cipher_iv_length(your_algorithm)
        )
    );
```

your_algorithm - for example 'AES-256-CBC'

#### What is initialization vector

An IV is generally a random number that guarantees the encrypted text is unique.

To explain why it's needed, let's pretend we have a database of people's names encrypted with the key 'secret' and no IV.

1 John dsfa9p8y098hasdf
2 Paul po43pokdfgpo3k4y
3 John dsfa9p8y098hasdf

If John 1 knows his cipher text (dsfa9p8y098hasdf) and has access to the other cipher texts, he can easily find other people named John.

Now in actuality, an encryption mode that requires an IV will always use one. If you don't specify an IV, it's automatically set to a bunch of null bytes. Imagine the first example but with a constant IV (00000000).

1 John dsfa9p8y098hasdf 00000000
2 Paul po43pokdfgpo3k4y 00000000
3 John dsfa9p8y098hasdf 00000000

To prevent repeated cipher texts, we can encrypt the names using the same 'secret' key and random IV's:

1 John sdf875n90mh28458 86714561
2 Paul fg9087n5b60987nf 13541814
3 John gjhn0m89456vnler 44189122

As you can see, the two 'John' cipher texts are now different. Each IV is unique and has influenced the encryption process making the end result unique as well. John 1 now has no idea what user 3's name is.