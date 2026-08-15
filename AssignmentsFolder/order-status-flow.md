# Order Status Flow

**Support Deflection MVP — Northstar Retail Co.**
**Prepared by:** Group 34
**Date:** 14/08/2026

---

This document explains, in full, everything that happens when a customer sends a message about their order status. It covers every decision point, every possible outcome, and the exact reply text the bot sends.

## The decision tree

```
                Order-status message detected
                             |
                             v
              Order number found in the message?
                 No |                    | Yes
                     v                    v
        Ask the customer         Order ID exists in our data?
        for their order number       No |             | Yes
                                          v             v
                              Reply: order not     Check the order's
                              found — flag it       status value
                              for a human                 |
                     --------------------------------------------------
                     |            |             |            |        |
                     v            v             v            v        v
                 Shipped     Processing     Delivered    Cancelled  Other /
                                                                     unrecognized
                Reply:        Reply:         Reply:        Reply:    Flag it
              carrier + ETA  not shipped   already        order      for a
                              yet          delivered     cancelled   human
```

## Step-by-step: what the bot does

### Step 1: A message gets classified as "order status"

Before this flow even starts, the bot has already checked the message text against a list of trigger words — things like "shipped," "tracking," "where is my order," and "delivered." If one of these words appears, the message enters the order-status flow described in this document.

### Step 2: Does the message contain an order number?

The bot scans every word in the message looking for something shaped like an order number — the letters "GP34" followed by digits, for example GP3410234. It checks each word individually and strips off punctuation like question marks first.

If no order number is found anywhere in the message, the bot does not guess. It stops and asks the customer directly for one. The conversation isn't finished at this point, but no human is needed yet either.

> **Reply when no order number is found**
> "Can you share your order number? It looks like GP3410234."

### Step 3: Does that order number exist in Northstar's data?

Assuming an order number was found, the bot looks it up against the order records. In this MVP, that's a small table of sample orders standing in for Northstar's real order system.

If the number isn't in the data — a typo, an old order, or a number from a different system — the bot does not pretend to know. It replies honestly and flags the ticket for a human to check.

> **Reply when the order number isn't found**
> "I couldn't find order [ID]. Let me get a person to help."

### Step 4: What does the order's status say?

If the order is found, the bot reads its status field and picks one of five paths. Four of them are answered directly. One is not.

#### Outcome 1: Shipped
The bot has a carrier name and an expected delivery date on file, so it shares both.

> **Auto-reply**
> "Order GP3410234 has shipped with UPS. Expected by Aug 13."

#### Outcome 2: Processing
The order hasn't shipped yet. The bot gives the expected ship date instead of a delivery date, so it isn't implying the package has already left.

> **Auto-reply**
> "Order GP3410235 hasn't shipped yet. Expected ship date: Aug 15."

#### Outcome 3: Delivered
The bot confirms delivery, but leaves the door open in case the customer disagrees — "I didn't get it" is a different problem than "where is it," and this reply invites that follow-up rather than closing the conversation.

> **Auto-reply**
> "Order GP3410236 was already delivered. Let us know if you didn't receive it."

#### Outcome 4: Cancelled
The bot states the fact plainly and proactively loops in a human, since a cancellation the customer wasn't expecting usually needs a real explanation the bot doesn't have.

> **Auto-reply**
> "Order GP3410238 was cancelled. I'll have a team member follow up."

#### Outcome 5: Other / unrecognized status
This is a safety net, not a normal outcome. If an order's status field holds something the bot doesn't recognize — a data entry error, a new status Northstar's system starts using later — the bot does not guess what it means. It hands the ticket to a human instead of risking a wrong answer.

> **Auto-reply**
> "I found the order but I'm not sure of its status. Routing to a person."

## Why it's built this way

- The bot only ever answers when it's confident — missing order number, unmatched order, and unrecognized status all fall back to asking or escalating instead of guessing.
- Four of five paths need no human at all. Only genuinely uncertain cases (not found, cancelled, unrecognized) involve a person.
- Every reply is a fixed template filled in with real data — nothing is generated freely, so every possible reply can be read and approved in advance.

## Known limitation

If the bot can't find an order number, it currently asks once and stops — it doesn't yet re-check the customer's next message for the number they provide. Wiring that follow-up connection is unbuilt and worth a board task if there's time.
