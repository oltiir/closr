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
- **Orders**: products with sizes, prices and stock; cash-on-delivery orders created straight from the chat.
- **Risk flags**: mark customers with failed or suspicious orders so agents confirm before shipping.
- **Channel simulator**: simulated channels and customers (with delay and failure rate) so the system can be
  demonstrated without real Meta/WhatsApp API access.

## Documentation

Work follows the order the course requires: conceptual model → SAD → DDD → code.

| Deliverable | Folder | Status |
|---|---|---|
| 1. Conceptual model (UML class diagram + description) | [`docs/01-conceptual-model`](docs/01-conceptual-model) | diagram drafted |
| 2. Software Architecture Document (SAD) | [`docs/02-sad`](docs/02-sad) | not started |
| 3. Detailed Design Document (DDD) | [`docs/03-ddd`](docs/03-ddd) | not started |
| 4. Implementation | [`backend/`](backend), [`frontend/`](frontend) | not started |

## Architecture

**Style: Layered (strict).** Each layer calls only the layer directly below it, and each module
runs through all three layers. The layers are separate .NET projects, so the compiler enforces the rule
(`Api → Business → Data`, never upwards).

```
┌──────────────────────────────────────────┐
│ Closr.Api       presentation             │  Web API controllers, SignalR hub
├──────────────────────────────────────────┤
│ Closr.Business  business logic           │  module services (I*Service), rules
├──────────────────────────────────────────┤
│ Closr.Data      data access              │  EF Core repositories, PostgreSQL
└──────────────────────────────────────────┘
```

Modules talk to each other only through their service interfaces in the business layer, and the
dependencies point one way: Inbox → Customers, Inbox → Assistant → Orders → Customers.

**Stack:** ASP.NET Core Web API · React (Vite) · PostgreSQL (EF Core / Npgsql)

**Design patterns:** Façade (each module's `I*Service`), Adapter (one `IChannel` for Instagram /
WhatsApp / simulator), Factory Method (choosing the channel adapter), Strategy (reply generation).

## Repository layout

```
closr/
├── docs/
│   ├── 01-conceptual-model/
│   ├── 02-sad/
│   └── 03-ddd/
├── backend/
│   ├── Closr.sln
│   ├── Closr.Api/          Controllers/{Inbox,Customers,Orders,Assistant}Controller.cs, Hubs/
│   ├── Closr.Business/     Inbox/  Customers/  Orders/  Assistant/
│   ├── Closr.Data/         ClosrDbContext.cs, Migrations/, Inbox/  Customers/  Orders/  Assistant/
│   └── Closr.Tests/
├── frontend/
│   └── src/modules/        inbox/  customers/  orders/  assistant/
└── docker-compose.yml      PostgreSQL for local development
```

Each module has the same folder name in every layer and in the docs, so a box in the SAD can be
traced straight to its code.

## Responsibilities

One module per member; each member commits their own module from their own GitHub account.

| Member | GitHub | Module | Packages / classes |
|---|---|---|---|
| Olti Ramadani | @oltiir | _TBD_ | _TBD_ |
| | | | |

Modules (one per member): **Inbox** (channels, conversations, messages) · **Orders** (products,
stock, COD orders) · **Customers** (profiles across channels, merge suggestions, risk flags) ·
**AI Assistant** (intent detection, reply suggestions). With 2 members: Inbox + Orders; 3: + Customers;
4: + AI Assistant.
Authentication, configuration, the channel simulator and the project skeleton are shared work and do not
count as a module.
