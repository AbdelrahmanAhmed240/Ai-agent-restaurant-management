# AI Agent Restaurant Management

An AI-powered restaurant management automation built with **n8n**.

The system uses an AI Agent to handle customer interactions through WhatsApp, answer restaurant-related questions, create and manage orders, validate order information, and store confirmed orders.

## Current Features

- WhatsApp AI ordering
- Restaurant menu Q&A
- Menu and item information retrieval
- Order creation and confirmation
- Cart building and price calculation
- Combo and sauce handling
- Order ID generation
- Google Sheets order storage
- Order lookup and customer verification
- Order modification
- Order cancellation
- Delivery and payment validation

## Architecture

```text
                         ┌──────────────────┐
                         │     WhatsApp     │
                         └────────┬─────────┘
                                  │
                                  ▼
                         ┌──────────────────┐
                         │     Webhook      │
                         └────────┬─────────┘
                                  │
                                  ▼
                         ┌──────────────────┐
                         │    AI Router     │
                         └────────┬─────────┘
                                  │
              ┌───────────────────┼───────────────────┐
              │                   │                   │
              ▼                   ▼                   ▼
       ┌─────────────┐     ┌─────────────┐     ┌─────────────┐
       │  Questions  │     │   Orders    │     │   General   │
       │  Assistant  │     │  Assistant  │     │  Assistant  │
       └─────────────┘     └──────┬──────┘     └─────────────┘
                                  │
                                  ▼
                         ┌──────────────────┐
                         │     AI Agent     │
                         └────────┬─────────┘
                                  │
                    ┌─────────────┴─────────────┐
                    │                           │
                    ▼                           ▼
          ┌──────────────────┐        ┌─────────────────────────────┐
          │  Knowledge Base  │        │       Order Tools           │
          │                  │        │                             │
          │ Supabase Vector  │        │  build_cart                 │
          │      Store       │        │  Calculate_tool             │
          └──────────────────┘        │  orders_generate_id         │
                                      │  normalize_order_identity   │
                                      │  validate_order_modification│
                                      └────────────┬────────────────┘
                                                   │
                                                   ▼
                                          ┌─────────────────┐
                                          │  Google Sheets  │
                                          │  Order Storage  │
                                          └────────┬────────┘
                                                   │
                                                   ▼
                                          ┌─────────────────┐
                                          │ WhatsApp Reply  │
                                          └─────────────────┘
