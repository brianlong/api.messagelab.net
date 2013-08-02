Message Lab
===========
I am starting a new project to enhance Internet email by solving certain problems and adding built-in features that should have been there in the first place.

Here are the problems that I think need to be solved or features that should always be included for effective email / messaging:

1. Less junk mail! The current system, and the Internet in general, are clogged up with junk email. A new email protocol will prevent junk mail from being delivered.
2. Delivery confirmations. At our office, we receive phone calls weekly from customers who did not receive an email we sent. It appears that their email was lost on the Internet. All messages sent should receive responses indicating the delivery status.
3. Integration with CRM / corporate transaction systems. I would like a simple REST API that I can use to integrate our company email into our transaction and CRM systems. All email sent to or from a customer should be attached to a customer record, in an easy to read format, regardless of who sent it or where it was sent from. Current email implementations are very weak in this regard.
4. Privacy while traveling the Internet. I want to be assured of secure point-to-point communications from my server to the recipient's server.
5. Managing and synchronizing email handling rules between my mail clients should be seamless and just work.
6. Elegant presentation and threading of conversations. Currently, long threaded conversations can be very difficult to read due to repeated signature blocks and messages. A new system should be able to parse the conversation and signature blocks to present the thread in an elegant manner.
7. I would like to be able to manage all of my email accounts from a single interface.
8. Digital signatures should be standard to help prevent phishing attacks and assure the recipient that my message was actually from me.
9. Support for encryption via OpenGPG should be built-in.
10. Companies should be able to set company-wide email rules that are enforceable across all email clients for all employees. The rules might be for corporate policies or government regulation.

Are there other problems or features that should be listed here? What else should I add to this list? You can comment in the Issues tracker here on GitHub (Please use the Comment Thread), on Twitter @brianlong, or on FaceBook (if you know me there). Thanks!

Definitions
===========
* Address: A User's unique Message Address in the same format as an email address (e.g. john.doe@example.com)
* Contact List: A list of Addresses, Signatures, Post Keys, and GPG Keys related to other people or organizations.
* GPG (Gnu Privacy Guard) Key: A way for two Users to encrypt or digitally sign Messages. The exchange of GPG keys is optional.
* Handshake: A process between two Users to verify that they wish to exchange Messages. The Handshake process includes an exchange of Post Keys. The exchange of GPG keys is optional.
* Message: A message sent from one User to another via a Server.
* Post Key: A unique key required to post Messages to another User's Server.
* Server: The machine that will send and receive Messages on the behalf of a User.
* Signature: A User's contact information available by making a request to the User's server (and by including the Post Key).
* User: A person or machine who wants to exchange Messages with other Users.

Sample Use
==========
Before exchanging messages, two Users will need to exchange Post Keys through a Handshake process. Anne will send a Handshake request to Bob's Address including a unique Post Key for Bob to use when he sends Messages to Anne's Address. Bob will then respond to Anne including a unique Post Key for Anne to use when she sends Messages to Bob. The two Post Keys will be unique and exclusive to each pair of User Addresses. In the event that a Post Key is compromised, Anne and Bob can simply repeat the Handshake process and replace the old Post Keys with new.

After the Handshake, Anne and Bob will be able to exchange messages. They can also use their Post Key request the other's signature to receive updated contact information.

Any messages that do not include the correct Post Key will be rejected by the User's Server. This should prevent junk messages from ever being a problem.

The API features SSL encryption for all interaction, so the plain text of a message is not revealed out on the Internet.

API
===
To accomplish these goals, I am planning a two-tiered system using HTTPS and REST APIs with a traditional web architecture. This upper tier of service will wrap legacy email so messages can be exchanged with others regardless of the system they are on. This API only discusses the upper tier. Programmers will be required to wrap their own legacy email infrastructure as required by their environment.

The Message Labs API is implemented as JSON or XML over HTTP using all four verbs (GET/POST/PUT/DELETE). Every resource, like Handshake or Message, has their own URL and are manipulated in isolation. We will follow the REST principles as much as we can, however some operations such as PUT or DELETE may be no-ops since Messages are immutable or the User may not be properly authorized.

You can explore the view part of the API (everything that's fetched with GET) through a regular browser. Using Firefox for this is particularly nice as it has a good, simple XML renderer. For example: /signatures.xml?a=USER_ADDRESS&pk=POST_KEY for XML or /signatures.json?a=USER_ADDRESS&pk=POST_KEY for JSON.

Exchanging Handshakes Between Servers
=====================================
* `POST /handshakes.format?a=user.name&pk=POST_KEY` creates a new Handshake request on the recipient's Server.

If Anne accepts Bob's Handshake, she will post a Handshake to Bob's server for him to accept.

See the [Handshake Schema](https://github.com/brianlong/api.messagelab.com/blob/master/schemas/handshakes.md) for the data included in a Handshake request.

Exchanging Messages Between Servers
===================================
* `POST /messages.format?a=user.name&pk=POST_KEY` creates a new Message on the recipient's Server.

The recipient's Server will verify that the sender's Address and Post Key match. If they are correct, the Server will respond with an HTTP status code of "200 OK" to indicate success. This status code will also serve as confirmation of delivery. If the User Address and Post Key do not match, the Message is discarded and the Server will return an HTTP status code of "401 Unauthorized"

All [HTTP Status Codes](http://en.wikipedia.org/wiki/List_of_HTTP_status_codes) will be supported and returned by the Server where appropriate.

See the [Message Schema](https://github.com/brianlong/api.messagelab.com/blob/master/schemas/messages.md) for the data included in a Message.

User Authentication On Our Server
=================================
When you're using the API, it's always through an existing User. There's no special API user. So when you use the API as "John Doe", you get to see and work with what "John Doe" is allowed to see and do. Authenticating is done with an authentication token, which you'll find on the User Profile screen of our website.

When using the authentication token, you don't need a separate password. But since Moving Leads uses HTTPS & Basic Authentication, and lots of implementations assume that you want to have a password, it's often easier just to pass in a dummy password, like X.

Here's an authentication example using curl:

    curl -u 605b32dd:X https://messagelab.net/signatures/USER_ADDRESS.xml&pk=POST_KEY
    
Remember that anyone who has your authentication token can see and change everything you have access to. So you want to guard that as well as you guard your username and password. If you come to fear that it has been compromised, you can regenerate it at any time from the User Profile screen in customers.movingleads.com.

MORE TO FOLLOW...
=================
