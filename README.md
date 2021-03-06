# PHP hash "collisions"

Register with *password 1* and then sign in with *password 2*. If you're in then the storage uses specified algorithm to hash the password and PHP uses `==` to compare them.

## [MD5](md5.md) and [SHA-1](sha1.md)
For **MD5** and **SHA-1**, it uses the long-known trick (it actually is a documented feature, see [*PHP type comparison tables*](https://php.net/types.comparisons) & [*Floating point numbers*](https://php.net/types.float)) that for PHP `'0e1' == '00e2' == '0'`, it just uses it for *practical* purposes. Any password *matches* any other password from the list.

## [Plaintext](plaintext.md)
For **plaintext**, it uses various conversion tricks. First password will *match* just the second one.

### Conclusion
Use `===` when comparing anything in PHP, not `==`. And use [`password_hash()`](https://php.net/function.password-hash) and [`password_verify()`](https://php.net/function.password-verify) for password hashing in PHP, don't use MD5 or SHA-1.

### History
It all started with [this tweet](https://twitter.com/spazef0rze/status/439352552443084800), I've generated `QNKCDZO` and `240610708` in February 2014 and it has since spread all over the intertubes. Just [google it](https://www.google.cz/search?q=%22QNKCDZO%22).

- MD5: [Tweet](https://twitter.com/spazef0rze/status/439352552443084800), [code](http://3v4l.org/2vrMi)
- SHA-1: [Tweet](https://twitter.com/spazef0rze/status/523010190900469760), [code](http://3v4l.org/tT4l8)
- Plaintext: [Tweet](https://twitter.com/spazef0rze/status/522882677452832768), [code](http://3v4l.org/K3ljr)
