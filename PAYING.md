# Giving your agent a wallet

Your agent found something worth buying and told you it cannot pay. That is
correct behaviour, not a fault: Panscia issues a Lightning invoice, and an agent
can only settle it if someone has given it a wallet to spend from.

An agent cannot obtain a wallet by itself. Funding takes money, and money takes a
human. What follows is how to hand one over.

## What the agent actually needs

One capability: **pay a BOLT11 invoice**. That is the whole requirement.

- No Panscia account, no API key, no registration with us
- No preimage handling — send `Authorization: L402 <invoice_id>` and the node
  confirms settlement itself
- No integration with our code; we issue standard invoices, deliberately

If your agent can already pay a Lightning invoice, it can already buy on the
network.

## Who holds it

Whoever runs the agent. We never hold buyers' funds and do not want to — that
would make us a custodian of your money, with everything that implies.

So the wallet is yours, and so are the limits on it.

## Choosing one

Any Lightning wallet your agent can call will do. What to look for:

- **An API or MCP interface** the agent can invoke — a wallet with only a
  human-facing UI cannot be driven by an agent
- **Small amounts supported.** Per-query prices are low, so a wallet with a high
  minimum payment will not be usable for most of the network
- **Funding you control**, kept separate from anything larger

Custodial wallets are a reasonable trade for a spending float holding small
amounts, and a poor one for savings. Self-custodial wallets are the reverse.
Either works here — the network only ever sees an invoice being paid.

## Set a spending cap

Give the agent the smallest balance that makes it useful, and a per-purchase
limit if your wallet supports one. An agent with an unbounded wallet is a bad
idea regardless of how much you trust the network it is buying from — mistakes,
loops and bad judgement all cost real money at machine speed.

Top it up deliberately rather than connecting it to your main funds.

## What we have observed

An agent without a wallet does the sensible thing: it surfaces the invoice and
the price and asks you to decide. We have seen this in both chat and agentic
sessions — the agent understood it needed a wallet, said so plainly, and handed
the invoice over.

Whether a given client can *drive* a wallet once you have provided one varies by
client, and we have not tested them all. If you try it, we would like to know
what happened.

## Paying by hand

Perfectly reasonable while you are evaluating. Pay the invoice with any Lightning
wallet, tell the agent it is settled, and it will retry the download. Payment and
delivery are separate steps by design, so a human can stand between them.
