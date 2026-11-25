# Closr

A shared inbox and lightweight CRM for small shops that sell through social media and messaging apps
(Instagram, Facebook, WhatsApp). Every customer message from every channel lands in one place,
the shop's agents answer it with AI-suggested replies, and a chat turns into a confirmed cash-on-delivery
order without leaving the conversation.

Course project for **Dizajni i Sistemit të Softuerit** (UBT, 2026).

## The problem

A typical local online shop sells from an Instagram page and a WhatsApp number. Orders arrive as chat
messages, the same customer writes from two different accounts, prices and sizes are repeated by hand
hundreds of times a day, and fake or unreachable cash-on-delivery orders cost real money in returned parcels.

## What Closr does

- **Unified inbox**: one conversation list across all connected channel accounts, assigned to agents.
- **Customer identity**: one customer profile across channels, with suggested merges when the same phone,
  email or name shows up on another handle.
- **AI assistant**: suggested replies with detected intent and confidence; the agent accepts or edits them.
- **Sales**: a deal pipeline per conversation, products with sizes and stock, COD orders with order items.
- **Risk flags**: mark customers with failed or suspicious orders so agents confirm before shipping.
- **Notes and tasks** on customers and conversations.
- **Channel simulator**: simulated channels and customers (with delay and failure rate) so the system can be
  demonstrated without real Meta/WhatsApp API access.

## Documentation

Work follows the order the course requires: conceptual model → SAD → DDD → code.

| Deliverable | Folder | Status |
|---|---|---|
| 1. Conceptual model (UML class diagram + description) | [`docs/01-conceptual-model`](docs/01-conceptual-model) | diagram drafted |
| 2. Software Architecture Document (SAD) | [`docs/02-sad`](docs/02-sad) | not started |
| 3. Detailed Design Document (DDD) | [`docs/03-ddd`](docs/03-ddd) | not started |
| 4. Implementation | `src/` | not started |

## Responsibilities

One module per member; each member commits their own module from their own GitHub account.

| Member | GitHub | Module | Packages / classes |
|---|---|---|---|
| Olti Ramadani | @oltiir | _TBD_ | _TBD_ |
| | | | |

Candidate modules (pick as many as there are members): **Inbox** (channels, conversations, messages),
**Customers** (profiles, identities, merge suggestions), **AI Assistant** (reply suggestions, intent),
**Sales** (products, deals, orders), **Risk** (risk flags, order confirmation).
Authentication, configuration and the architecture skeleton are shared work and do not count as a module.
