# 📘 Epic: Checkout & Payment Processing

---

## Epic Metadata

```yaml
epic_name: "Checkout & Payment Processing"
epic_id: "EPIC-004"
bounded_context: "Checkout"
status: "draft"
owner: "Checkout Team"
```

---

## Epic Overview

This epic enables users to complete secure purchases through guest or authenticated checkout flows, with address validation, payment processing via Cashfree, payment failure recovery, and order confirmation.

**Strategic Importance:**
- Final conversion step (KPI-001: 30% target, KPI-002: <60s target)
- Revenue realization point
- Integrates payment gateway, address validation, and order creation
- Critical for user trust and security (PCI-DSS compliance)

---

## Features in This Epic

| Feature ID | Feature Name | Status | Dependencies |
|------------|--------------|--------|--------------|
| FE-013 | Guest Checkout | Draft | FE-009, FE-002 |
| FE-014 | Address Validation | Draft | FE-013 or FE-003 |
| FE-015 | Payment Processing | Draft | FE-013 or FE-001 |
| FE-016 | Payment Failure Recovery | Draft | FE-015 |
| FE-017 | Order Confirmation | Draft | FE-015 |

---

## Success Criteria

1. ✅ Guest users can checkout without account creation
2. ✅ Addresses validated via Shiprocket before order placement
3. ✅ Payments processed securely via Cashfree (PCI-DSS)
4. ✅ Payment failures allow retry/method change without losing order
5. ✅ Order confirmation emails sent immediately
6. ✅ `OrderPlaced`, `PaymentConfirmed`, `PaymentFailed` events emit

---

## History & Status

* **Status:** Draft
* **Epic Created:** 2025-12-30
