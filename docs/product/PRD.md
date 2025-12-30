# 📘 Product Requirements Document (PRD)

**Version:** `1.0.0` | **Status:** `Draft`

## Table of Contents

1. Document Information
2. Governance & Workflow Gates
3. Feature Index (Living Blueprints)
4. Product Vision
5. Core Business Problem
6. Target Personas & Primary Use Cases
7. Business Value & Expected Outcomes
8. Success Metrics / KPIs
9. Ubiquitous Language (Glossary)
10. Architectural Overview (DDD – Mandatory)
11. Event Taxonomy Summary
12. Design System Strategy (MCP)
13. Feature Execution Flow
14. Repository Structure & File Standards
15. Feature Blueprint Standard (Stories & Gherkin Scenarios)
16. Traceability & Compliance Matrix
17. Non-Functional Requirements (NFRs)
18. Observability & Analytics Integration
19. Feature Flags Policy (Mandatory)
20. Security & Compliance
21. Risks / Assumptions / Constraints
22. Out of Scope
23. Rollout & Progressive Delivery
24. Appendix

---

## 1. Document Information

| Field              | Details                                |
| ------------------ | -------------------------------------- |
| **Document Title** | `itsme.fashion Strategic PRD`          |
| **File Location**  | `docs/product/PRD.md`                  |
| **Version**        | `1.0.0`                                |
| **Date**           | `2025-12-30`                           |
| **Author(s)**      | `Product Team`                         |
| **Stakeholders**   | `Product, Engineering, Business Leads` |

---

## 2. Governance & Workflow Gates

Delivery is enforced through **explicit workflow gates**.
Execution may be human-driven, agent-driven, or hybrid.

| Gate | Name                    | Owner                | Preconditions                             | Exit Criteria            |
| ---- | ----------------------- | -------------------- | ----------------------------------------- | ------------------------ |
| 1    | Strategic Alignment     | Product Architecture | Vision, context map defined               | Approval recorded        |
| 2    | Blueprint Bootstrapping | Planning Function    | Feature issues created, blueprints linked | Blueprint complete       |
| 3    | Technical Planning      | Engineering          | DDD mapping, flags defined                | Ready for implementation |
| 4    | Implementation          | Engineering          | Code + tests                              | CI green                 |
| 5    | Review                  | Engineering          | Preview deployed                          | Acceptance approved      |
| 6    | Release                 | Product / Ops        | All checks passed                         | Production approved      |

---

## 3. Feature Index (Living Blueprints)

_This section will be populated as features are defined in the roadmap._

| Feature ID | Title | GitHub Issue | Blueprint Path | Status |
| ---------- | ----- | ------------ | -------------- | ------ |
| TBD        | TBD   | TBD          | TBD            | TBD    |

---

## 4. Product Vision

> **Empower people to express their uniqueness with premium, clean, and cruelty-free beauty products delivered through a fast, trustworthy, and elegant shopping experience.**

itsme.fashion is a premium beauty ecommerce platform that offers ethically-sourced cosmetics, skin care, and hair care products emphasizing natural ingredients, sustainable manufacturing, and a bold brand identity. The platform prioritizes user autonomy, transparency, and seamless digital experiences.

---

## 5. Core Business Problem

**Problem Statement:**

Current beauty ecommerce platforms fall short in three critical dimensions:

1. **Ethical Transparency Gap** — Users cannot easily verify product ingredients, ethical sourcing, or cruelty-free claims during their purchase journey.

2. **Fragmented User Experience** — Shopping across mobile and desktop is inconsistent, with poor session persistence, slow checkout flows, and limited order visibility.

3. **Trust Deficit** — Consumers face uncertainty around payment security, shipping reliability, and product authenticity.

**Why This Matters:**

- 73% of beauty consumers prefer brands with clear ethical positioning
- Mobile commerce represents 60%+ of beauty product purchases
- Cart abandonment rates exceed 70% in ecommerce when trust signals are weak

**What Success Looks Like:**

A unified platform where users can discover, evaluate, and purchase ethical beauty products confidently, with full order visibility and seamless cross-device continuity.

---

## 6. Target Personas & Primary Use Cases

| Persona                      | Description                                                                         | Goals                                                                        | Key Use Cases                                                     |
| ---------------------------- | ----------------------------------------------------------------------------------- | ---------------------------------------------------------------------------- | ----------------------------------------------------------------- |
| **Conscious Beauty Shopper** | 25–40 years old, values ethical consumption, researches ingredients before purchase | Find cruelty-free and natural products; verify ethical claims; fast checkout | Browse by ethical markers, review ingredients, save to wishlist   |
| **Mobile-First Buyer**       | 18–35 years old, shops primarily on mobile, expects instant gratification           | Quick product discovery, one-tap checkout, order tracking                    | Search products, add to cart, complete purchase, track shipments  |
| **Returning Customer**       | Loyal user, reorders favorite products regularly                                    | Fast repurchase, manage multiple addresses, review order history             | View order history, reorder, update addresses, receive promotions |

---

## 7. Business Value & Expected Outcomes

| Outcome                              | Description                                                      | KPI Alignment    | Priority |
| ------------------------------------ | ---------------------------------------------------------------- | ---------------- | -------- |
| **Increase Conversion Rate**         | Reduce cart abandonment through trust signals and streamlined UX | KPI-001, KPI-002 | High     |
| **Expand Mobile Revenue Share**      | Optimize mobile experience to capture majority of transactions   | KPI-003          | High     |
| **Strengthen Brand Differentiation** | Position as leader in ethical beauty ecommerce                   | KPI-004          | High     |
| **Improve Customer Retention**       | Enable seamless reordering and personalized experiences          | KPI-005          | Medium   |
| **Operational Efficiency**           | Automate order fulfillment and notification workflows            | KPI-006          | Medium   |

---

## 8. Success Metrics / KPIs

| KPI ID    | Name                          | Definition                                              | Baseline | Target | Source                |
| --------- | ----------------------------- | ------------------------------------------------------- | -------- | ------ | --------------------- |
| `KPI-001` | Cart-to-Purchase Conversion   | (Completed Orders / Carts Created) × 100                | 15%      | 30%    | GA4 + Firestore       |
| `KPI-002` | Checkout Flow Completion Time | Median time from cart to order confirmation             | 180s     | 60s    | GA4                   |
| `KPI-003` | Mobile Transaction Share      | (Mobile Orders / Total Orders) × 100                    | 45%      | 65%    | GA4                   |
| `KPI-004` | Ethical Product Discovery     | % of sessions viewing cruelty-free/vegan filtered pages | 10%      | 40%    | GA4                   |
| `KPI-005` | Repeat Purchase Rate          | (Users with 2+ orders / Total users) × 100              | 12%      | 35%    | Firestore Analytics   |
| `KPI-006` | Order Fulfillment Automation  | % of orders auto-processed without manual intervention  | 60%      | 95%    | OTEL + Shiprocket API |

---

## 9. Ubiquitous Language (Glossary)

All domain terms **must be defined once and reused consistently**.

- **Aggregate** — A cluster of domain objects (entities and value objects) treated as a single unit for data changes.
- **Bounded Context** — A logical boundary within which a particular domain model is defined and applicable.
- **Cart** — A temporary collection of products selected by a user before checkout.
- **Checkout** — The process of finalizing a purchase, including address, payment, and order confirmation.
- **Command** — An imperative operation that changes system state (e.g., AddToCart, PlaceOrder).
- **CQRS** — Command Query Responsibility Segregation; separating write (commands) and read (queries) models.
- **Cruelty-Free** — Products not tested on animals, verified by certification or brand policy.
- **Domain Event** — A record of a significant business occurrence (e.g., OrderPlaced, PaymentConfirmed).
- **Event Sourcing** — Storing state changes as a sequence of events rather than current state snapshots.
- **Order** — A confirmed purchase including products, shipping address, payment method, and status.
- **Product** — A beauty item available for purchase (cosmetic, skin care, or hair care).
- **Query** — A read-only operation to retrieve data (e.g., GetProductCatalog, GetOrderHistory).
- **Shipment** — Physical delivery of an order managed by a shipping carrier.
- **Wishlist** — A saved collection of products a user intends to purchase later.

---

## 10. Architectural Overview (DDD — Mandatory)

The platform follows **Domain-Driven Design (DDD)** with **CQRS** and **Event Sourcing** patterns.

### Bounded Contexts

| Context         | Purpose                                                                            | Core Aggregate | Entities                              | Value Objects                             |
| --------------- | ---------------------------------------------------------------------------------- | -------------- | ------------------------------------- | ----------------------------------------- |
| **Catalog**     | Manage product inventory, metadata, and categorization (authoritative stock)       | Product        | Product, Category                     | SKU, Price, IngredientList, StockQuantity |
| **Cart**        | Handle shopping cart operations with server-side anonymous session persistence     | Cart           | CartItem                              | Quantity, ProductReference, SessionToken  |
| **Checkout**    | Process order placement, payment, and address validation (supports guest checkout) | Order          | OrderItem, ShippingAddress, GuestInfo | PaymentMethod, OrderStatus                |
| **Fulfillment** | Coordinate shipment creation and webhook-driven tracking updates                   | Shipment       | ShipmentItem, TrackingEvent           | TrackingNumber, CarrierInfo               |
| **Identity**    | Authenticate users and manage profiles                                             | User           | UserProfile, Address                  | Email, PasswordHash                       |
| **Wishlist**    | Store saved products for authenticated users with real-time sync                   | Wishlist       | WishlistItem                          | ProductReference                          |

### Context Interactions

- **Catalog → Cart:** Product data is referenced (not duplicated) in cart items; stock events control checkout availability
- **Cart → Checkout:** Cart is transformed into an Order on checkout initiation; price changes trigger user notification
- **Checkout → Fulfillment:** OrderPlaced event triggers shipment creation; OrderCanceled event halts fulfillment
- **Fulfillment → Checkout:** Webhook-driven tracking updates cached in Order aggregate
- **Identity → Checkout:** Optional authentication (guest checkout supported)

### Order Lifecycle State Machine

```
Pending Payment → Payment Failed → [Retry or Cancel]
Pending Payment → Payment Confirmed → Processing → Shipped → Delivered
Processing → Canceled (user-initiated, before shipment)
Delivered → Return Requested → Refund Issued (within 14 days)
```

### Returns & Refunds Policy

- **Return Window:** 14 days from delivery date
- **Condition:** Unopened products only (hygiene compliance)
- **Refund Method:** Full refund to original payment method
- **Process:** User initiates return request → Manual review → Pickup scheduled → Refund processed after product verification

---

## 11. Event Taxonomy Summary

| Event Name                | Producer Context | Consumers                    | Trigger Aggregate |
| ------------------------- | ---------------- | ---------------------------- | ----------------- |
| `ProductCreated`          | Catalog          | -                            | Product           |
| `ProductUpdated`          | Catalog          | Cart (for price sync)        | Product           |
| `ProductOutOfStock`       | Catalog          | Cart (for checkout blocking) | Product           |
| `CartItemAdded`           | Cart             | Analytics                    | Cart              |
| `CartPriceChanged`        | Cart             | Notification                 | Cart              |
| `CartAbandoned`           | Cart             | Marketing, Analytics         | Cart              |
| `OrderPlaced`             | Checkout         | Fulfillment, Notification    | Order             |
| `OrderCanceled`           | Checkout         | Fulfillment, Notification    | Order             |
| `PaymentConfirmed`        | Checkout         | Fulfillment                  | Order             |
| `PaymentFailed`           | Checkout         | Notification                 | Order             |
| `PaymentRetryRequested`   | Checkout         | Payment Gateway              | Order             |
| `ShipmentCreated`         | Fulfillment      | Notification, Checkout       | Shipment          |
| `ShipmentDispatched`      | Fulfillment      | Notification                 | Shipment          |
| `ShipmentTrackingUpdated` | Fulfillment      | Notification, Checkout       | Shipment          |
| `UserRegistered`          | Identity         | Marketing, Analytics         | User              |
| `WishlistItemAdded`       | Wishlist         | Analytics                    | Wishlist          |
| `WishlistSyncRequested`   | Wishlist         | Cross-device sessions        | Wishlist          |

---

## 12. Design System Strategy (MCP)

All UI must use a **design system delivered via MCP**.

| Parameter         | Value                         |
| ----------------- | ----------------------------- |
| **MCP Server**    | `@itsme/design-system-mcp`    |
| **Design System** | `itsme.fashion Design System` |
| **Component Lib** | Lit-based Web Components      |

Raw HTML/CSS is prohibited unless explicitly approved in a Feature Blueprint.

**Rationale:** MCP-driven design systems ensure:

- Consistent visual language across features
- Atomic component reusability
- Centralized styling updates without feature-level rework

---

## 13. Feature Execution Flow

**Diagram Required**

- Format: **Mermaid**
- Location: `docs/diagrams/feature-execution-flow.mermaid`

_Diagram will be generated during roadmap phase to visualize feature dependencies._

---

## 14. Repository Structure & File Standards

Source of truth is **GitHub**.

```text
/
├── .github/
│   ├── skills/                 # Agent skills
│   └── workflows/              # CI/CD pipelines
├── docs/
│   ├── product/                # PRD, Roadmap
│   ├── features/               # Feature blueprints
│   ├── epics/                  # Epic definitions
│   └── diagrams/               # Mermaid diagrams
├── src/
│   ├── frontend/               # Lit components
│   ├── services/               # DDD microservices
│   │   ├── catalog/
│   │   ├── cart/
│   │   ├── checkout/
│   │   ├── fulfillment/
│   │   ├── identity/
│   │   └── wishlist/
│   └── shared/                 # Cross-cutting concerns
```

---

## 15. Feature Blueprint Standard

Each feature blueprint **must include**:

1. **Metadata** (issue URL, status, bounded context)
2. **Deployment Plan** (Feature Flag defined)
3. **Stories (Vertical Slices)**
4. **Scenarios — Gherkin (Mandatory)**

### Gherkin Format

All user-facing behavior must be specified using Gherkin:

```gherkin
Feature: <Feature Name>

  Scenario: <Scenario Name>
    Given <initial context>
    When <action>
    Then <expected outcome>
```

**Example:**

```gherkin
Feature: Add Product to Cart

  Scenario: User adds available product to cart
    Given a user is viewing a product with SKU "SKIN-001"
    And the product is in stock
    When the user clicks "Add to Cart"
    Then the cart count increments by 1
    And a confirmation message displays "Added to cart"
```

---

## 16. Traceability & Compliance Matrix

_To be populated during feature blueprint phase._

| Feature ID | Flag ID | Flag Key | Bounded Context | Status |
| ---------- | ------- | -------- | --------------- | ------ |
| TBD        | TBD     | TBD      | TBD             | TBD    |

---

## 17. Non-Functional Requirements (NFRs)

| Metric                       | ID        | Target                           | Tool                |
| ---------------------------- | --------- | -------------------------------- | ------------------- |
| **Page Load Time (P95)**     | `NFR-001` | < 2s                             | Lighthouse, OTEL    |
| **API Response Time (P95)**  | `NFR-002` | < 500ms                          | OTEL                |
| **Availability**             | `NFR-003` | 99.9% uptime                     | GCP Monitoring      |
| **Mobile Performance Score** | `NFR-004` | > 90 (Lighthouse)                | Lighthouse          |
| **PWA Installability**       | `NFR-005` | PWA score > 90                   | Lighthouse          |
| **Offline Cart Access**      | `NFR-006` | Read-only cart available offline | Service Worker      |
| **Security Compliance**      | `NFR-007` | PCI-DSS for payments             | Cashfree compliance |
| **Accessibility**            | `NFR-008` | WCAG 2.1 Level AA                | Automated testing   |
| **Data Residency**           | `NFR-009` | India (GCP us-central1)          | GCP IAM             |

---

## 18. Observability & Analytics Integration

Mandatory tooling (parameterized):

- **Analytics:** `Google Analytics 4 (GA4)`
- **Telemetry:** `OpenTelemetry (OTEL)`
- **Logs:** Structured JSON logs via Cloud Logging
- **Metrics:** Custom metrics tracked in OTEL and GCP Monitoring
- **Traces:** Distributed tracing across microservices

**Instrumentation Requirements:**

- All GraphQL resolvers must emit spans
- All domain events must be logged with correlation IDs
- All user interactions must fire GA4 events

---

## 19. Feature Flags Policy (Mandatory)

### Naming Convention (Enforced)

```
feature_fe_[feature_issue]_fl_[flag_issue]_[context]_enabled
```

**Example:**

```
feature_fe_42_fl_43_checkout_enabled
```

### Lifecycle

1. **Creation:** Flag created before feature development starts
2. **Development:** Feature built behind flag (default: disabled)
3. **Testing:** Flag enabled in staging environment
4. **Rollout:** Gradual rollout in production (10% → 50% → 100%)
5. **Cleanup:** Flag removed after 30 days at 100% and KPIs stable (within 10% of target)

### Tooling

- **Provider:** Firebase Remote Config
- **SDK:** Firebase Admin SDK (backend), Firebase JS SDK (frontend)

---

## 20. Security & Compliance

| Requirement            | Implementation                                                  |
| ---------------------- | --------------------------------------------------------------- |
| **Authentication**     | Firebase Authentication (email/password) + guest checkout       |
| **Authorization**      | Firestore Security Rules + custom claims (user & guest context) |
| **Payment Security**   | PCI-DSS compliant via Cashfree                                  |
| **Data Encryption**    | At rest (Firestore default), in transit (HTTPS)                 |
| **Input Validation**   | Server-side validation in all command handlers                  |
| **Address Validation** | Shiprocket serviceability check before order confirmation       |
| **Rate Limiting**      | Cloud Functions concurrency limits + API throttling             |
| **Audit Logging**      | All state changes logged as domain events                       |

**Compliance:**

- GDPR (if serving EU users): Right to erasure, data portability
- Consumer Protection Act (India): Transparent pricing, refund policies

---

## 21. Risks / Assumptions / Constraints

| Type           | Description                                                  | Mitigation                                       |
| -------------- | ------------------------------------------------------------ | ------------------------------------------------ |
| **Risk**       | Cashfree payment gateway downtime                            | Display fallback message, allow payment retry    |
| **Risk**       | Payment failures require order state "pending payment"       | Implement order state machine with timeout logic |
| **Risk**       | Shiprocket API rate limits during high traffic               | Implement queue-based shipment creation          |
| **Risk**       | Shiprocket address validation latency adds checkout friction | Cache validation results, implement timeout      |
| **Risk**       | Firebase cold starts impacting checkout latency              | Use min instances for critical functions         |
| **Risk**       | Stock-out race condition between cart and checkout           | Atomic stock check during order placement        |
| **Assumption** | Users have stable internet for real-time cart sync           | PWA with service worker for offline cart access  |
| **Assumption** | Product catalog < 10,000 SKUs in first year (internal stock) | Use Firestore collections; plan for sharding     |
| **Assumption** | Price change notifications acceptable UX friction            | Alert user, require confirmation before checkout |
| **Constraint** | Must use Firebase for hosting and authentication             | Locked into GCP ecosystem                        |
| **Constraint** | Limited to Node.js 22.x for Cloud Functions                  | Ensure compatibility with npm packages           |
| **Constraint** | INR only (single currency)                                   | Price modeling simplified, no FX complexity      |

---

## 22. Out of Scope

**Explicitly excluded from initial release:**

- Multi-language support (only English in v1)
- Social login (Google, Facebook OAuth)
- Product reviews and ratings
- Loyalty points or rewards program
- Subscription-based product deliveries
- Live chat support
- Advanced analytics dashboards for admins
- Mobile native apps (iOS/Android)
- Partial order cancellations (full order cancellation only)
  **Future consideration (post-MVP):**

- AI-powered product recommendations
- AR virtual try-on for cosmetics
- Influencer collaboration features

---

## 23. Rollout & Progressive Delivery

### Phased Rollout Strategy

1. **Internal Alpha (Week 1–2)**

   - Deploy to staging environment
   - Internal team testing with feature flags at 100%
   - Goal: Validate core workflows end-to-end

2. **Limited Beta (Week 3–4)**

   - Deploy to production with flags at 10%
   - Invite 50–100 beta users
   - Goal: Gather feedback, monitor performance metrics

3. **General Availability (Week 5+)**
   - Gradual rollout: 25% → 50% → 100%
   - Monitor KPIs daily
   - Goal: Full public launch with rollback capability

### Rollback Plan

- All features gated by flags
- If critical issue detected: disable flag immediately
- Incident response SLA: < 15 minutes to disable feature

---

## 24. Appendix

### References

- [Firebase Documentation](https://firebase.google.com/docs)
- [GraphQL Mesh](https://the-guild.dev/graphql/mesh)
- [Domain-Driven Design (Evans)](https://www.domainlanguage.com/ddd/)
- [Cashfree API Docs](https://docs.cashfree.com/)
- [Shiprocket API Docs](https://apidocs.shiprocket.in/)

### Supporting Documents

- `README.md` — Repository overview
- `.github/skills/` — Agent skill definitions
- (Future) `docs/diagrams/` — Architecture and flow diagrams