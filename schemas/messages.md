Messages
==========
Messages include:
* Post Key
* ID
* Original ID to use for threading
* From Address
* TO Addresses
* CC Addresses
* BCC Addresses
* Subject
* Body in plain text
* Body in HTML
* Body CSS for HTML
* Original Message ID (for replies)
* Date & Time Sent (UTC)
* File Attachments

Messages should by sent by POST to `https://messagelab.net/handshakes.xml?a=user.address` for XML or `https://messagelab.net/handshakes.json?a=user.address` for JSON.

It is the responsibility of the Sender's server to POST the Message to each recipient's Address and Server using the appropriate Post Key. A good User interface will automatically suggest the Exchange of Handshakes for any CC Addresses not currently in the User's contact list.

**XML POST (TO ANOTHER SERVER):**

``` xml
<message>
  <post_key>Post Key</post_key>
  <id>Globally Unique Message ID from the Sender's Server</id>
  <original_id>The Original Message ID to use for threading</original_id>
  <from>From Address</from>
  <to_addresses>
    <to>To Address</to>
    ...
  </to_addresses>
  <cc_addresses>
    <cc>CC Address</cc>
    ...
  </cc_addresses>
  <bcc_addresses>
    <bcc>BCC Address</bcc>
    ...
  </bcc_addresses>
  <subject>Subject</subject>
  <body_text>The Body of the message in text format</body_text>
  <body_html>The body of the message in HTML format</body_html>
  More ...
  <sent_at>Date and Time Sent by Server (UTC)</sent_at>
</message>
```

**XML RESPONSE:**
HTTP Status Code 200 OK or 401 Unauthorized.

**JSON POST (TO ANOTHER SERVER):**
``` json
{
  "message":
  {
    "post_key":"The Post Key to use when sending Messages to the Sender.",
    "from":"The Sender's Address",
    More ...
  }
}
```

**JSON RESPONSE:**

HTTP Status Code 200 OK or 401 Unauthorized.

Messages are immutable, so PUT (edit) and DELETE (delete) are not supported. Only the recipients can read Messages.