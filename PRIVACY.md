# Privacy (summary)

The authoritative, full policy is at <https://mytesla.io/privacy>. This is a
short summary for quick auditing.

## What we do **not** do

- We **do not store** your vehicle's location, drive history, or charge history
  beyond serving the live request.
- We **do not sell** your data.
- We **do not train** AI models on your conversations or vehicle data.
- We **never receive** your Tesla password (authorization is via Tesla's OAuth).

## What we keep

Only what's needed to run the service: your account (email), subscription and
usage records, and the encrypted Tesla OAuth tokens required to send the
commands you ask for. Tesla tokens are encrypted at rest (AES-256-GCM) and
rotated on refresh.

We also keep two identifiers from your Tesla connection:

- **Your Tesla account identifier** (the ID Tesla assigns your login, not your
  password), kept with your Tesla connection.
- **Your vehicles' VINs**, so support can see which cars an account covers,
  plus a keyed one-way hash of each VIN (not the VIN itself). The hash is used
  only to notice when two accounts share the same car or Tesla login; it
  alerts our team and blocks nothing.

All of it is erased when you delete your account. Retention details are in the
full policy.

## Your prompts

Your natural-language prompts are handled by **your own AI client**, not by
mytesla.io. We receive the specific tool calls your assistant decides to make —
not the raw conversation.

## Control

You can revoke mytesla.io's access to your Tesla at any time from your Tesla
account's third-party-apps settings, and remove the connector from your AI
client. Either action immediately stops any further access.

Questions: **support@mytesla.io**.
