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
credit-ledger records, and the encrypted Tesla OAuth tokens required to send the
commands you ask for. Tesla tokens are encrypted at rest (AES-256-GCM) and
rotated on refresh.

## Your prompts

Your natural-language prompts are handled by **your own AI client**, not by
mytesla.io. We receive the specific tool calls your assistant decides to make —
not the raw conversation.

## Control

You can revoke mytesla.io's access to your Tesla at any time from your Tesla
account's third-party-apps settings, and remove the connector from your AI
client. Either action immediately stops any further access.

Questions: **privacy@mytesla.io**.
