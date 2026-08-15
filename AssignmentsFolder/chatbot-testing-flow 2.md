# Chatbot Testing Flow

**Support Deflection MVP — Northstar Retail Co.**
**Prepared by:** Group 34
**Date:** 14/08/2026

---

This document explains how the chatbot will be tested before it's considered ready to demo or hand off. It focuses on the order status and returns branches from the Chatbot Decision Flow.

## What we're testing for

- Does the bot sort each message into the correct branch?
- For order status (auto-resolved), is the exact reply correct — not just close?
- For returns, does the bot correctly resolve what it can on its own, and only hand off to a human when it genuinely can't (a failed refund)?
- Does the bot correctly remember what step of a conversation it's on — returns now takes several messages back and forth, not just one?
- Do the edge cases fail safely — asking for more info or flagging a human — instead of giving a wrong or made-up answer?

## The test flow

```
        Pick a test conversation
                |
                v
        Run it through the bot,
        message by message
                |
                v
      Compare actual vs. expected
      at every step, not just the end
                |
        -----------------
        |               |
        v               v
      Pass            Fail
        |               |
        v               v
   Log it as        Log what broke +
   passing           add a fix task
                      to the board
                          |
                          v
                    Retest after
                     the fix ships
```

Returns tests are now conversations, not single messages — a test only passes if every step along the way replies correctly, not just the final message.

## Where results get recorded

A shared test log with one row per test:

| Column | What goes in it |
|---|---|
| Test ID | A short reference, e.g. T-01 |
| Input | The message, or full sequence of messages for a returns conversation |
| Expected branch / path | Order status, or which returns path (A/B/C/D) |
| Actual result | What the bot actually did at each step |
| Pass / Fail | Pass only if every step matches, not just the last one |
| Notes | What broke, if anything, and why |

## Test cases to run

### Order status branch
| ID | Input | Expected outcome |
|---|---|---|
| T-01 | "Where is my order GP3410234?" | Auto-reply: shipped, carrier + ETA |
| T-02 | "Order status for GP3410235?" | Auto-reply: still processing, ship date |
| T-03 | "Any update on GP3410238?" | Auto-reply: cancelled, human flagged |
| T-04 | "Where's my order?" (no order number) | Bot asks for the order number |
| T-05 | "Where is order GP3499999?" (doesn't exist) | Bot says not found, flags a human |

### How to read the returns test cases

Returns tests aren't single messages — they're short conversations, because the bot now asks follow-up questions instead of resolving everything in one reply. The steps are written as an arrow chain, for example:

`"return an item" → A → yes → GP3410236 → yes`

Each item after the first message is what the tester types back to the bot at that point in the conversation. The letters A, B, C, D are not something the tester invents — they're the exact menu options the bot itself lists when the returns flow starts:

```
What do you need help with?
  A) Return an item
  B) Check refund status
  C) How long do I have to return something?
  D) Something else
```

So `A` means the tester replied "A" to pick "Return an item," `B` means they picked "Check refund status," and so on. Everything after a letter (like `yes`, or an order number) is the tester's answer to whatever question the bot asked next.

### Returns branch — Section A: Return an item
| ID | Conversation | Expected outcome |
|---|---|---|
| T-06 | "I want to return something" → A → yes → GP3410236 → yes | Eligible: bot gives the 4 return steps, no human needed |
| T-07 | Same, but answer "no" to condition | Not eligible: bot explains why (must be unused, tags/packaging) |
| T-08 | Same, but use order GP3410239 (delivered 44 days ago) | Not eligible: bot explains the 30-day window has expired |
| T-09 | "return an item" → A → yes → GP3499999 | Order not found, bot offers to try again or go back to menu |
| T-10 | "return an item" → A → no | Bot explains where to find the order number, no dead end |

### Returns branch — Section B: Check refund status
| ID | Conversation | Expected outcome |
|---|---|---|
| T-11 | "check refund status" → B → GP3410239 | Reply: refund not started yet |
| T-12 | "check refund status" → B → GP3410236 | Reply: refund in progress |
| T-13 | "check refund status" → B → GP3410240 | Reply: refund completed, exact amount and date |
| T-14 | "check refund status" → B → GP3410241 | Refund failed — this is the one case that hands off to a human |

### Returns branch — Sections C and D, and navigation
| ID | Conversation | Expected outcome |
|---|---|---|
| T-15 | "refund policy" → C | Bot gives the 30-day policy text, no order number needed |
| T-16 | "return an item" → D | Bot re-shows the menu instead of guessing what they meant |
| T-17 | Mid-flow, type "menu" | Bot jumps back to the returns menu from anywhere in the conversation |

### Priority / overlap edge cases
| ID | Input | Expected outcome |
|---|---|---|
| T-18 | "I want to return my order, has it even shipped yet?" (mentions both return and shipping) | Returns wins — this is a deliberate rule, not a bug, and should be checked on purpose |

## Pass / fail rules

- **Pass**: every step of the conversation matches the expected reply, not just the final one.
- **Fail**: wrong branch, wrong data in a reply, the bot losing track of which step it's on, or — the most serious kind — the bot answering confidently (approving a return, stating a refund amount) when it shouldn't.
- A fail where the bot invents or wrongly approves something counts as high priority, above fails where it just asks an unnecessary question.

## Known risk areas worth extra testing

- **Keyword priority**: returns/refunds keywords are checked before order-status keywords, so any message mentioning both needs to be tested on purpose, not by accident — see T-18.
- **Order number not in the system**: covered in T-05 and T-09, but worth re-running after any change to the order data file.
- **Losing conversation state**: because returns is now multi-step, there's a new failure mode that didn't exist before — the bot forgetting which step it's on, or carrying over an order number from a previous conversation into a new one. Worth testing "menu" and "quit" mid-flow specifically, not just the happy path.
- **The only human handoff in returns is a failed refund (T-14)**: everything else should resolve on its own. If any other path unexpectedly hands off to a human, that's a fail, not a safe fallback.

## After testing

Every failed test becomes its own board task, sized under 4 hours, with the failing test ID referenced in the task so the fix can be checked against the same test afterward. Testing isn't done once — it's done once every test in this document passes, including re-runs after fixes.
