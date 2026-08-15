# Workflow Mechanics & Operational Principles

**Core Routing Engine**
The **Router Chain** evaluates incoming WhatsApp messages and directs them to one of three specialized handlers:
* **General Assistant**: Manages simple greetings and pleasantries.
* **Questions Assistant**: Queries the Supabase Vector KB for menu items, pricing, and operating details.
* **Orders Assistant**: Enforces business logic and invokes specialized tools to create, calculate, or modify orders.

---

**Order Execution Flow**
* **New Orders**: `build_cart` (validates schema) ➔ `Calculate_tool` (computes EGP total) ➔ `orders_generate_id` (creates `ORD-XXXXXXXX-XXX`) ➔ `orders_sheet_write` (appends to Google Sheets).
* **Modifications & Cancellations**: `normalize_order_identity` (sanitizes Egyptian phone numbers) ➔ `validate_order_modification` (enforces `< 30 min` window in `Africa/Cairo` and `In Kitchen` status) ➔ `edit_tool` (updates order record).

---

**Security & Data Guardrails**
* **Strict Price Verification**: Prices cannot be assumed by the agent; all item rates must originate from the Vector DB.
* **State Enforcement**: Blocked modification attempts immediately prevent downstream calls to calculation or editing tools.
* **Privacy Guard**: Internal logic, database schemas, and other customers' order records are strictly concealed.