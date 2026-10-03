# Privacy (summary)

The authoritative, full policy is at <https://mytesla.io/privacy>. This is a
short summary for quick auditing.

## What we do **not** do

- We **do not store** your vehicle's location, drive history, or charge history
  beyond serving the live request.
- We **do not sell or resell** your data.
- We **do not train** AI models on your conversations or vehicle data.
- We **never receive** your Tesla password (authorization is via Tesla's OAuth).

## What we keep

What we keep to run the service and keep it reliable includes: your account
(email), subscription and credit-ledger records, a log of each tool call (which
tool, whether it succeeded, any error code or diagnostic note, latency, credits
used; kept 12 months), and the encrypted Tesla OAuth tokens required to send
the commands you ask for. Tesla tokens are encrypted at rest (AES-256-GCM) and
rotated on refresh. We also keep an approximate location for your account,
taken from your browser's IP address when you sign in or open your dashboard
(only the latest one), bug reports you choose to file, and where your sign-up
came from.

From your Tesla connection we also keep two identifiers:

- **Your Tesla account identifier** (the ID Tesla assigns your login, not your
  password), kept with your Tesla connection.
- **Your vehicles' VINs**, so support can see which cars an account covers,
  plus a keyed one-way hash of each VIN (not the VIN itself). The hash is used
  only to notice when two accounts share the same car or Tesla login; it
  alerts our team and blocks nothing.

These identifiers and the location are erased when you delete your account.
The full policy lists everything we keep and for how long.

## Usage analytics

Our servers send Google Analytics usage events: one for each request to the
connector, one for each tool call, and a few account events (connecting,
sign-up, new subscription, bug report filed). Tool-call and account events are
keyed to an internal account ID rather than your email; connector requests are
keyed to a code computed from the connecting IP address and user agent with a
secret key only we hold. Events can include the approximate city of the
computer that connects to us. They contain no prompts, no Tesla tokens, no car
names or VINs, and none of the data your commands return, such as your car's
location or battery level; a failed call carries only a short error label. We
use them only to keep the service reliable, improve its quality, understand how
it is used, and see which channels bring new users and paid subscriptions, and
we never sell or resell them. The full policy lists exactly what an event can
contain.

## Your prompts

Your natural-language prompts are handled by **your own AI client**, not by
mytesla.io. We receive the specific tool calls your assistant decides to make —
not the raw conversation.

## Control

You can revoke mytesla.io's access to your Tesla at any time from your Tesla
account's third-party-apps settings, and remove the connector from your AI
client. Either action immediately stops any further access.

Questions: **support@mytesla.io**.
