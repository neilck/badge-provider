# badge-provider
This repository implements a Badge Provider, that automates the awarding of Nostr badges when called by client applications.

## Workflow

**Badge Award Request from Client to Badge Provider**

Clients maintain a list of badge providers containing
  1. Badge definition event address pointer (30009:<public key>:identifier)
  2. Badg Provider URL

The client directs a user to obtain a badge by redirecting to badge provider, including an NIP-98 HTTP Auth event in the header.

This header is signed by the user, to verify who is requesting the badge.

In addition to "u" and "method" tags, the HTTP Auth event MUST also contain a "redirectURL" tag.

**Badge Provider Processing**

As per NIP-98, badge provider should perform validation checks.

Badge provider MAY check the redirectURL against a whitelist.

After running custom logic, badge provider calls the redirectURL as an HTTP POST call with an NIP-98 HTTP Auth event, with signed badge award event as JSON in body.

**Client Receiving Badge Award**

After verifying HTTP Auth event, and verifying signed event using provider's public key, client has record or publish badge award event to relays.



