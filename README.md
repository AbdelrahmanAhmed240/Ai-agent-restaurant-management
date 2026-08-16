# 🤖 AI Agent Restaurant Management

![n8n](https://img.shields.io/badge/Automation-n8n-FF6D5A?logo=n8n)
![WhatsApp](https://img.shields.io/badge/Messaging-WhatsApp-25D366?logo=whatsapp)
![Supabase](https://img.shields.io/badge/Vector%20Database-Supabase-3ECF8E?logo=supabase)
![Google Sheets](https://img.shields.io/badge/Data%20Store-Google%20Sheets-34A853?logo=googlesheets)
![AWS](https://img.shields.io/badge/Cloud-AWS-232F3E?logo=amazonaws)
![Coolify](https://img.shields.io/badge/Deployment-Coolify-6B46C1?logo=coolify)

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
