Message Lab
===========
I am starting a new project to enhance Internet email by solving certain problems and adding built-in features that should have been there in the first place.

Here are the problems that I think need to be solved or features that should always be included for effective email / messaging:

1. Less junk mail! The current system, and the Internet in general, are clogged up with junk email. A new email protocol will prevent junk mail from being delivered.
2. Delivery confirmations. At our office, we receive phone calls daily from customers who did not receive an email we sent. It appears that their email was lost on the Internet. All messages sent should receive responses indicating the delivery status.
3. Integration with CRM / corporate transaction systems. I would like a simple REST API that I can use to integrate our company email into our transaction and CRM systems. All email sent to or from a client should be attached to a client record, in an easy to read format, regardless of who sent it or where it was sent from. Current email implementations are very weak in this regard.
4. Privacy while traveling the Internet. I want to be assured of secure point-to-point communications from my server to the recipient's server.
5. Managing and synchronizing email handling rules between my mail clients should be seamless and just work.
6. Elegant presentation and threading of conversations. Currently, long threaded conversations can be very difficult to read due to repeated signature blocks and messages. A new system should be able to parse the conversation and signature blocks to present the thread in an elegant manner.
7. I would like to be able to manage all of my email accounts from a single interface.
8. Digital signatures should be standard to help prevent phishing attacks and assure the recipient that my message was actually from me.
9. Support for encryption via GPG should be built-in.
10. Companies should be able to set company-wide email rules that are enforceable across all email clients for all employees. The rules might be for corporate policies or government regulation.

Are there other problems or features that should be listed here? What else should I add to this list? You can comment in the Issues tracker here on GitHub (Please use the Comment Thread) or on Twitter @brianlong. Thanks!

API
==================
To accomplish these goals, I am planning a two-tiered system using HTTPS and REST APIs with a traditional web architecture. This upper tier of service will wrap legacy email so messages can be exchanged with others regardless of the system they are on.

The API for advanced email is pending...
