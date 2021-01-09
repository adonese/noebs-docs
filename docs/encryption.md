## Encryption in noebs


While noebs offers a strong support for encryption through different sdk libraries (java, dart, js), user's can still roll out their own encryption.


- Get [Public Key from here](/#api-request-sample)
- In `Key` api response, we are interested in `pubKeyValue`, which is the public key for encrpytion
- Concatenate `UUID` + `IPIN`
- Use RSA encrypt `UUID` + `IPIN` and encrypt them with the `pubKeyValue`

(More technical details here copied from EBS docs):

### Cipher specification
-	Cipher algorithm: RSA
-	Cipher mode: ECB
-	Padding : PKCS1Padding

### Example:

```
Clear value = "0000"
UUID = "550e8400-e29b-41d4-a716-446655440000"
Encrypted value = Base64.encode(RSAencrypt("550e8400-e29b-41d4-a716-446655440000"+ "0000 ", publicKeyValue))
```


!!! note
    Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nulla et euismod
    nulla. Curabitur feugiat, tortor non consequat finibus, justo purus auctor
    massa, nec semper lorem quam in massa.