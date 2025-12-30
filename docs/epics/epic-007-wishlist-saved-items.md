# 📘 Epic: Wishlist & Saved Items

---

## Epic Metadata

```yaml
epic_name: "Wishlist & Saved Items"
epic_id: "EPIC-007"
bounded_context: "Wishlist"
status: "draft"
owner: "Wishlist Team"
```

---

## Epic Overview

This epic enables authenticated users to save products for later with real-time cross-device synchronization and quick cart conversion.

---

## Features in This Epic

| Feature ID | Feature Name | Status | Dependencies |
|------------|--------------|--------|--------------|
| FE-023 | Wishlist Management | Draft | FE-001, FE-004 |
| FE-024 | Wishlist Real-Time Sync | Draft | FE-023 |
| FE-025 | Wishlist to Cart | Draft | FE-023, FE-008 |

---

## Success Criteria

1. ✅ Users add/remove wishlist items
2. ✅ Wishlist syncs across devices in real-time
3. ✅ Users move wishlist items to cart
4. ✅ `WishlistItemAdded`, `WishlistSyncRequested` events emit

---

## History & Status

* **Status:** Draft
* **Epic Created:** 2025-12-30
