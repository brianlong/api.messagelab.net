Handshakes
==========
Handshakes include:
* ID from the sender's Server
* Sender's Address
* Post Key to use when sending Messages to Sender
* GPG Key to use for encryption (optional)

Handshakes should by sent by POST to `https://messagelab.net/handshakes.xml?a=user.address` for XML or `https://messagelab.net/handshakes.json?a=user.address` for JSON.

**XML POST (TO ANOTHER SERVER):**

``` xml
<handshake>
  <id>Globally Unique Handshake ID from the Sender's Server</id>
  <address>The Sender's Address</address>
  <post_key>The Post Key to use when sending Messages back to the Sender.</post_key>
  <gpg_public_key>The GPG public key to use when encrypting Messages to the Sender (optional)</pgp_pubic_key>
</handshake>
```

**XML RESPONSE:**
HTTP Status Code 200 OK .

**JSON POST (TO ANOTHER SERVER):**
``` json
{
  "handshake":
  {
    "id:"Globally Unique Handshake ID from the Sender's Server",
    "address":"The Sender's Address",
    "post_key":"The Post Key to use when sending Messages to the Sender.",
    "gpg_public_key":"The GPG public key to use when encrypting Messages to the Sender (optional)"
  }
}
```

**JSON RESPONSE**
HTTP Status Code 200 OK.

Handshakes are immutable, so PUT (edit) and DELETE (delete) are not supported.