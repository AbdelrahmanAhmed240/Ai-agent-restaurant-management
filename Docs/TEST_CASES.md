# Test Suite: Baraka Restaurant AI System

### Group 1: Intent Routing
* **1.1 General Greeting**: `"السلام عليكم، ازيك؟"` ➔ Routes to `General Assistant` ➔ Returns greeting without tool execution.
* **1.2 Menu Query**: `"ايه مكونات وجبة البركة و بكام؟"` ➔ Routes to `Questions Assistant` ➔ Queries Supabase Vector DB for price/ingredients.
* **1.3 New Order**: `"عايز اطلب 2 وجبة بركة"` ➔ Routes to `Orders Assistant` ➔ Initiates order workflow.

---

### Group 2: Order Creation
* **2.1 Valid Order Execution**: User provides items, address, and phone ➔ Executes `build_cart` ➔ `Calculate_tool` ➔ `orders_generate_id` ➔ Appends to Google Sheets via `orders_sheet_write` (`In Kitchen` status).
* **2.2 Malformed Cart**: Input `{"items": []}` ➔ Throws `EMPTY_CART` exception ➔ Halts execution before calculation.

---

### Group 3: Modifications & Cancellations
* **3.1 Valid Change Window (< 30 min)**: Time elapsed = 15 min (`In Kitchen`) ➔ `validate_order_modification` returns `allowed: true` ➔ Recalculates total and executes `edit_tool`.
* **3.2 Expired Window (≥ 30 min)**: Time elapsed = 35 min ➔ `validate_order_modification` returns `allowed: false` ➔ Refuses changes; blocks `edit_tool`.
* **3.3 Invalid Status**: Status = `Out for Delivery` ➔ Rejects modification request.

---

### Group 4: Security & Edge Cases
* **4.1 System Security Guard**: User asks for internal DB/other customer orders ➔ Rejects query with standard privacy refusal.
* **4.2 Phone Normalization**: Inputs `+201012345678`, `01012345678`, or `201012345678` ➔ `normalize_order_identity` standardizes all to `1012345678`.