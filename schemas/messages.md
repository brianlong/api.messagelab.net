Messages
==========
Messages include:
* Post Key
* Sender ID (Sender's message ID)
* Original ID to use for threading & replies
* Headers
* DKIM
* SPF
* Junk Score
* Junk Description
* Charset
* From Address
* TO Addresses
* CC Addresses
* BCC Addresses
* Subject
* Body in plain text
* Body in HTML
* Attachments
* File Attachments
* Date & Time Sent (UTC)

Messages should by sent by POST to `https://messagelab.net/handshakes.xml?a=user.address` for XML or `https://messagelab.net/handshakes.json?a=user.address` for JSON.

It is the responsibility of the Sender's server to POST the Message to each recipient's Address and Server using the appropriate Post Key. A good User interface will automatically suggest the Exchange of Handshakes for any CC Addresses not currently in the User's contact list.

**XML POST (TO ANOTHER SERVER):**

``` xml
<message>
  <post_key>Post Key</post_key>
  <sender_id>Globally Unique Message ID from the Sender's Server</sender_id>
  <original_id>The Original Message ID to use for threading & replies</original_id>
  <headers>
    <header>Contents of a single header record</header>
    <header>...</header>
  </headers>
  <dkim>Domain Keys results & signatures</dkim>
  <spf>Sender Policy Framework verification</spf>
  <junk_score>Junk Mail Score</junk_score>
  <junk_description>Junk Mail Description</junk_description>
  <charset>Character set used in the message</charset>
  <from>From Address</from>
  <to_addresses>
    <to>To Address</to>
    <to>...</to>
  </to_addresses>
  <cc_addresses>
    <cc>CC Address</cc>
    <cc>...</cc>
  </cc_addresses>
  <bcc_addresses>
    <bcc>BCC Address</bcc>
    <bcc>...</bcc>
  </bcc_addresses>
  <subject>Subject</subject>
  <body_text>The Body of the message in text format</body_text>
  <body_html>The body of the message in HTML format</body_html>
  <attachments>
    <attachement>
      <path>Location of temp file on server</path>
      <mime_type>Mime Type</mime_type>
    </attachement>
    <attachment>...</attachment>
  </attachments>
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
    "sender_id":"Globally Unique Message ID from the Sender's Server",
    "original_id":"The Original Message ID to use for threading",
    "headers":{
      "header":"Contents of a single header record",
      "header":"..."
    },
    "dkim":"Domain Keys results & signatures",
    "spf":"Sender Policy Framework verification",
    "junk_score":"Junk Mail Score",
    "junk_description":"Junk Mail Description",
    "charset":"Character set used in the message",
    "from":"The Sender's Address",
    "to_addresses":{
      "to":"To Address",
      "to":"..."
    },
    "cc_addresses":{
      "cc":"CC Address",
      "cc":"..."
    },
    "bcc_addresses":{
      "bcc":"BCC Address",
      "bcc":"..."
    },
    "subject":"Subject",
    "body_text":"Body in Text format",
    "body_html":"Body in HTML format",
    "attachments":{
      "attachment":"path to file",
      "mime_type":"MIME Type"
    },
    "sent_at":"Date and Time Sent by Server (UTC)"
  }
}
```

**JSON RESPONSE:**
HTTP Status Code 200 OK or 401 Unauthorized.

**OTHER VERBS:**

Messages are immutable, so PUT (edit) is not supported.

DELETE (delete) will only be supported for a User's own message store.

Only the recipients can read Messages.