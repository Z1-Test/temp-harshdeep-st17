# Project Clarifications

> **Status:** ✅ All clarifications resolved and integrated into PRD v1.0.0
> **Last Updated:** 2025-12-30

## Resolution Summary

All 14 ambiguities have been clarified and integrated into the PRD. The following decisions were made:

## Q1: Product Returns & Refunds Policy

The PRD mentions "Consumer Protection Act (India): Transparent pricing, refund policies" but does not define return/refund behavior.

**Decision Required:**

- [x] **Full refunds within N days** — Products can be returned within a fixed period (e.g., 7, 14, 30 days) with full refund
- [ ] **Store credit only** — Returns are accepted but refunds are issued as store credit, not cash
- [ ] **No returns on opened beauty products** — Due to hygiene/safety, only unopened products can be returned
- [ ] **Case-by-case manual review** — All return requests require human approval
- [ ] Other: [Please specify]

**Why This Matters:**  
This decision affects order state modeling, payment reversal workflows, inventory management, and compliance obligations.

---

## Q2: Inventory Management Authority

The PRD references product stock status ("product is in stock") but does not clarify who manages inventory and where stock truth resides.

**Decision Required:**

- [x] **itsme.fashion owns inventory** — Platform maintains authoritative stock counts in Firestore
- [ ] **Third-party warehouse/ERP integration** — Stock truth lives in external system (e.g., warehouse management system)
- [ ] **Hybrid model** — Some products owned, some dropshipped/3rd-party
- [ ] Other: [Please specify]

**Why This Matters:**  
This decision determines whether the Catalog bounded context is read-only (syncs from external) or write-authoritative, affecting overselling prevention, reservation logic, and data consistency models.

---

## Q3: Cart Persistence for Anonymous Users

The PRD specifies "session persistence" for shopping carts but does not define persistence behavior for anonymous (non-logged-in) users.

**Decision Required:**

- [ ] **Browser-only (localStorage)** — Anonymous cart persists only in the user's browser
- [x] **Server-side anonymous session** — Anonymous carts are stored server-side with session token
- [ ] **Anonymous carts expire** — Cart data is ephemeral and cleared after session timeout
- [ ] **Login required to save cart** — Cart is only persisted for authenticated users
- [ ] Other: [Please specify]

**Why This Matters:**  
This affects cross-device continuity, data privacy (GDPR), and whether Cart aggregate requires identity binding.

---

## Q4: Payment Failure Recovery

The PRD lists `PaymentFailed` as an event but does not define user recovery options.

**Decision Required:**

- [ ] **Automatic retry with same payment method** — System retries payment automatically
- [x] **User chooses: retry or change method** — Order is held, user can update payment details
- [ ] **Order canceled, cart restored** — Order is canceled, items returned to cart
- [ ] **Manual intervention required** — Support team contacts user
- [ ] Other: [Please specify]

**Why This Matters:**  
This decision affects order state transitions, payment gateway interaction patterns, and whether orders can exist in "pending payment" state.

---

## Q5: Wishlist Synchronization Across Devices

The PRD states wishlist is for "authenticated users" but does not clarify cross-device behavior.

**Decision Required:**

- [x] **Real-time sync** — Wishlist updates immediately reflected across all logged-in devices
- [ ] **Eventual consistency** — Updates propagate within seconds/minutes
- [ ] **Device-specific wishlist** — Each device has separate wishlist (no sync)
- [ ] Other: [Please specify]

**Why This Matters:**  
This determines whether Wishlist aggregate requires event-driven sync, optimistic UI updates, or conflict resolution logic.

---

## Q6: Product Price Changes for In-Cart Items

If a product's price changes after it is added to a cart, the PRD does not specify which price is honored.

**Decision Required:**

- [ ] **Price at checkout** — User pays the current price when placing order
- [ ] **Price at add-to-cart** — Price is locked when item is added to cart
- [x] **Notify user of price change** — System alerts user and requires confirmation
- [ ] **Cart auto-updates but order history preserves original** — Cart reflects new price, but order snapshots old price
- [ ] Other: [Please specify]

**Why This Matters:**  
This affects cart state modeling, revenue accuracy, and user trust. Different choices lead to different aggregate invariants (Cart vs Order).

---

## Q7: Shipment Tracking Data Authority

The PRD references "Real-time tracking link and status updates" via Shiprocket but does not clarify data authority.

**Decision Required:**

- [ ] **Shiprocket is source of truth** — Platform queries Shiprocket API for live status
- [x] **Webhook-driven updates** — Shiprocket pushes status changes, platform caches them
- [ ] **Platform stores snapshot only** — Tracking data stored once, not updated after shipment
- [ ] Other: [Please specify]

**Why This Matters:**  
This determines whether Fulfillment context is event-sourced, cache-invalidated, or read-through, and affects API rate limits and data staleness.

---

## Q8: User Address Validation

The PRD mentions "address validation" in checkout but does not specify validation strictness or source.

**Decision Required:**

- [ ] **No validation** — User can enter any address, delivery failure is their risk
- [ ] **Format validation only** — Basic checks (e.g., required fields, postal code format)
- [ ] **API-based validation** — Use third-party service (e.g., Google Maps API) to validate deliverability
- [x] **Shiprocket pre-validation** — Check if Shiprocket can deliver to address before order placement
- [ ] Other: [Please specify]

**Why This Matters:**  
This affects order rejection rates, user friction, and whether Checkout context must integrate external APIs synchronously.

---

## Q9: Multi-Currency or Single Currency

The PRD does not specify whether the platform supports multiple currencies or is INR-only.

**Decision Required:**

- [x] **INR only** — All transactions in Indian Rupees
- [ ] **Multi-currency support** — Users can select currency, prices dynamically converted
- [ ] **Display multi-currency, transact in INR** — Prices shown in local currency but payment in INR
- [ ] Other: [Please specify]

**Why This Matters:**  
This affects Catalog price modeling, payment gateway configuration, and whether pricing is a value object or an entity with currency state.

---

## Q10: Order Cancellation Policy

The PRD does not define whether users can cancel orders after placement, and under what conditions.

**Decision Required:**

- [x] **Cancel anytime before shipment** — Users can cancel orders until shipment is dispatched
- [ ] **Cancel within N hours** — Orders can be canceled within a fixed time window (e.g., 1 hour)
- [ ] **No cancellation allowed** — Once order is placed, cancellation requires support intervention
- [ ] **Partial cancellation supported** — Users can cancel individual items in an order
- [ ] Other: [Please specify]

**Why This Matters:**  
This affects order state machine design, payment reversal workflows, and whether Order aggregate must handle partial cancellations.

---

## Q11: Product Out-of-Stock Behavior

If a product goes out of stock while in a user's cart, the PRD does not specify handling.

**Decision Required:**

- [ ] **Remove from cart automatically** — Item is removed, user is notified
- [x] **Keep in cart, block checkout** — Item remains in cart but checkout is disabled
- [ ] **Notify user but allow checkout** — User can attempt to purchase (race condition possible)
- [ ] **Reserve stock on add-to-cart** — Stock is reserved when item is added (with expiration)
- [ ] Other: [Please specify]

**Why This Matters:**  
This determines whether Cart context must subscribe to Catalog events, and whether stock reservation is required (affecting Catalog aggregate invariants).

---

## Q12: Guest Checkout Support

The PRD mentions "authenticated users" for wishlists but does not clarify if checkout requires authentication.

**Decision Required:**

- [x] **Guest checkout allowed** — Users can place orders without creating an account
- [ ] **Login required for checkout** — Users must authenticate before placing orders
- [ ] **Guest checkout with optional account creation** — Users can checkout as guest, then optionally create account
- [ ] Other: [Please specify]

**Why This Matters:**  
This affects Identity context boundaries, whether Order aggregate requires a UserId, and impacts conversion rates (KPI-001).

---

## Q13: Feature Flag Removal Trigger

The PRD states flags are removed "after 30 days at 100% and no issues" but does not define "no issues."

**Decision Required:**

- [ ] **Zero incidents reported** — No user-reported bugs or system alerts
- [x] **KPIs stable** — Success metrics within expected ranges
- [ ] **Manual approval required** — Product/engineering sign-off needed
- [ ] **Automated based on metrics** — System auto-triggers removal if conditions met
- [ ] Other: [Please specify]

**Why This Matters:**  
This affects flag lifecycle automation and whether flag cleanup is human-gated or system-driven.

---

## Q14: Mobile App Strategy (Future Scope Clarification)

The PRD lists "Mobile native apps (iOS/Android)" as out of scope but references "Mobile-First Buyer" persona and 65% mobile transaction target.

**Decision Required:**

- [ ] **Mobile web only for MVP** — All mobile traffic uses responsive web app
- [ ] **Native apps planned for later phase** — Web-first, native apps post-MVP
- [x] **Progressive Web App (PWA)** — Installable web app with offline support
- [ ] Other: [Please specify]

**Why This Matters:**  
This clarifies whether PWA features (offline mode, push notifications) are in scope, affecting architecture decisions.

---

## Summary

**Total Ambiguities Detected:** 14

**Critical for Roadmap:** Q1, Q2, Q4, Q6, Q10, Q11, Q12  
**Critical for Architecture:** Q2, Q3, Q6, Q7, Q11  
**Critical for UX/Business:** Q1, Q4, Q8, Q12

**Recommendation:** Resolve all questions before proceeding to roadmap decomposition.
