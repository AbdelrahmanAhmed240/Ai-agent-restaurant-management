# 🤖 AI Agent Restaurant Management

![n8n](https://img.shields.io/badge/n8n-Automation-FF6D5A)
![WhatsApp](https://img.shields.io/badge/WhatsApp-Messaging-25D366)
![Supabase](https://img.shields.io/badge/Supabase-Vector%20Database-3ECF8E)
![Google%20Sheets](https://img.shields.io/badge/Google%20Sheets-Data%20Store-34A853)
![AWS](https://img.shields.io/badge/AWS-Cloud-232F3E)
![Coolify](https://img.shields.io/badge/Coolify-Deployment-6B46C1)

An autonomous end-to-end restaurant management system built on **n8n**. The system leverages an AI Router and specialized sub-assistants feeding into a central AI Agent to process WhatsApp conversations, handle dynamic menu Q&A via RAG, parse complex food choices (combos, sauces), build real-time carts, and manage order lifecycles—all stored seamlessly in Google Sheets.

---

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
              ┌─────────────────────┼─────────────────────┐
              │                     │                     │
              ▼                     ▼                     ▼
       ┌─────────────┐       ┌─────────────┐       ┌─────────────┐
       │  Questions  │       │   Orders    │       │   General   │
       │  Assistant  │       │  Assistant  │       │  Assistant  │
       └──────┬──────┘       └──────┬──────┘       └──────┬──────┘
              │                     │                     │
              └─────────────────────┼─────────────────────┘
                                    │
                                    ▼
                           ┌──────────────────┐
                           │     AI Agent     │
                           └────────┬─────────┘
                                    │
                    ┌───────────────┴───────────────┐
                    │                               │
                    ▼                               ▼
          ┌──────────────────┐            ┌──────────────────┐
          │  Knowledge Base  │            │   Order Tools    │
          │                  │            │                  │
          │ Supabase Vector  │            │ • build_cart     │
          │      Store       │            │ • Calculate_tool │
          └────────┬─────────┘            │ • generate_id    │
                   │                      │ • normalize_id   │
                   │                      │ • validate_mod   │
                   │                      └────────┬─────────┘
                   │                               │
                   │                               ▼
                   │                      ┌──────────────────┐
                   │                      │  Google Sheets   │
                   │                      │  (Order Storage) │
                   │                      └────────┬─────────┘
                   │                               │
                   └────────────────┬──────────────┘
                                    │
                                    ▼
                           ┌──────────────────┐
                           │  WhatsApp Reply  │
                           └──────────────────┘
