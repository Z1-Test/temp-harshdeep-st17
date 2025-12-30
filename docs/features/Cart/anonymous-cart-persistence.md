# 📄 Feature Specification: Anonymous Cart Persistence

## 0. Metadata

```yaml
feature_name: "Anonymous Cart Persistence"
bounded_context: "Cart"
status: "draft"
owner: "Cart Team"
```

## 1. Overview

Ensures anonymous user carts persist server-side across sessions using guest session tokens. Builds on guest session management to provide cart continuity.

## 3. Goals

**UX:** Carts persist for 30 days, seamless across page reloads  
**Business:** Reduce cart abandonment for non-registered users

## 5. Functional Scope

1. Link Cart aggregate to guest session token
2. Restore cart on session validation
3. 30-day TTL aligned with session expiration
4. Merge guest cart on user authentication

## 6. Dependencies

**Depends on:** FE-002 (Guest Session Management), FE-009 (Cart Management)

## 7. Key Scenarios

**Scenario 1.1:** Guest adds item → refreshes page → cart preserved  
**Scenario 1.2:** Guest closes browser → returns within 30 days → cart restored  
**Scenario 1.3:** Guest logs in → cart merged with authenticated cart

## 9. Implementation Tasks

- [ ] T01 — Associate Cart aggregate with guest session tokens
- [ ] T02 — Implement cart restoration logic on session load
- [ ] T03 — Cart TTL cleanup job for expired sessions
- [ ] T04 — Guest-to-authenticated cart merge on login
- [ ] T05 — Feature flag feature_fe_anoncart_fl_010_cart_enabled

## 11. Rollout

**Flag:** feature_fe_anoncart_fl_010_cart_enabled

## 12. History

* **Status:** Draft  
* **Related Epics:** EPIC-003
