# Web Crypto API

The **Web Crypto API** is an interface allowing a script to use cryptographic primitives in order to build systems using cryptography.

> **Warning:** The Web Crypto API provides a number of  low-level cryptographic primitives. It's very easy to misuse them, and  the pitfalls involved can be very subtle.

Even assuming you use the basic cryptographic functions correctly,  secure key management and overall security system design are extremely  hard to get right, and are generally the domain of specialist security  experts.

Errors in security system design and implementation can make the security of the system completely ineffective.

**If you're not sure you know what you are doing, you probably shouldn't be using this API.**

## Interfaces

Some browsers implemented an interface called [`Crypto`](https://developer.mozilla.org/en-US/docs/Web/API/Crypto) without having it well defined or being cryptographically sound. In  order to avoid confusion, methods and properties of this interface have  been removed from browsers implementing the Web Crypto API, and all Web  Crypto API methods are available on a new interface: [`SubtleCrypto`](https://developer.mozilla.org/en-US/docs/Web/API/SubtleCrypto). The [`Crypto.subtle`](https://developer.mozilla.org/en-US/docs/Web/API/Crypto/subtle) property gives access to an object implementing it.

## Specifications

![](https://github.com/ChickenKyiv/awesome-mozilla-web-articles/blob/master/main%20folder/images/article13-folder/t1.jpg)

## Browser compatibility

### `Crypto`

![](https://github.com/ChickenKyiv/awesome-mozilla-web-articles/blob/master/main%20folder/images/article13-folder/t2.jpg)