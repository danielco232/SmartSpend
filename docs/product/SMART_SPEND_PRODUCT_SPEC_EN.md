# SmartSpend - Product Specification

Version: 0.4

---

# 1. System Purpose

SmartSpend is a personal system for managing benefits, vouchers, gift cards, and membership-based benefits.

The purpose of the system is to allow the user to:

- Store all benefits and eligibility rights in one place.
- Know which benefits are available.
- Quickly find where they can be redeemed.
- Use benefits before they expire.

The system acts as a smart wallet for benefits and privileges.

---

# 2. System Vision

Users often have many different types of benefits:

- Gift cards.
- Vouchers.
- Consumer clubs.
- Permanent membership benefits.

The problem:

Users do not always know:

- That they have a certain benefit.
- Where the benefit can be used.
- Whether it is about to expire.
- Whether they have available money or discounts at a specific store.

SmartSpend connects benefit sources with redemption locations and presents the information at the right time.

---

# 3. Core Principles

## Search First

The main action in the system is searching by redemption location.

The main user question:

"Do I have something I can use here?"

Therefore, search focuses mainly on:

- Store.
- Brand.
- Provider.

---

## Mobile First

The system is designed primarily for mobile usage.

Focus:

- Android devices.
- Samsung Galaxy devices.
- One-handed usage.
- Minimal typing.

---

# 4. Core Concepts

## Provider

A Provider is an organization that manages, supplies, or grants a benefit or eligibility right.

A Provider can be connected to:

- Multiple benefits.
- Multiple redemption locations.

Examples:

- BUYME.
- Hever.
- Workplace benefit provider.

---

## Store

A Store is a place where a benefit or eligibility right can be redeemed.

Examples:

- FOX HOME.
- ACE.
- IKEA.
- KSP.

---

# 5. Benefit Types

SmartSpend supports three benefit types:

---

## 5.1 Gift Card

A benefit with monetary value.

Examples:

- BUYME 300 ₪.
- Store-specific gift card.

Properties:

- Monetary amount.
- Provider.
- One or multiple Stores.
- Expiration date.
- Link or image.

Future:

- Balance tracking.

---

## 5.2 Voucher

A voucher representing a right to use or redeem something.

Examples:

- FOX HOME voucher purchased through Hever.
- Restaurant voucher.

Properties:

- Provider.
- One or multiple Stores.
- Amount or usage conditions.
- Expiration date.

Important:

A voucher purchased through a club such as Hever is stored as Voucher and not as Membership.

---

## 5.3 Membership

A permanent eligibility right based on belonging to a club.

Examples:

- Hever.
- Other consumer clubs.

Properties:

- Provider.
- Multiple Stores.
- Changing discount conditions.

Example:

Membership:

Hever

Stores:

- FOX HOME.
- KSP.
- Restaurants.

---

# 6. Entity Relationships

General structure:

Provider

↓

Benefits

↓

Stores


Example:

BUYME

Gift Card 500 ₪

Stores:

- FOX HOME
- ACE
- IKEA


Example:

Hever

Membership

Stores:

- FOX HOME
- KSP
- Restaurants

---

# 7. Separation Between Benefit Source and Redemption Location

The system does not assume that the benefit source is the redemption location.

Example:

The user has:

BUYME 500 ₪

but wants to shop at FOX HOME.

The system should find:

BUYME → FOX HOME.

---

# 8. Home Screen

The Home Screen is the central area of the system.

Structure:

1. Search bar.
2. Expiring soon benefits.
3. Add benefit button.

There is no separate empty-state screen.

---

# 9. Expiring Soon Benefits

The system displays benefits that expire within 30 days.

Rules:

- Sorted by closest expiration date.
- Displayed horizontally.
- Includes position indicator.

Format:

<Current>/<Total>

Example:

<1/4>

---

If there are no expiring benefits:

"No benefits expire within the next 30 days."

---

# 10. Search

Search is performed by:

- Store.
- Brand.
- Provider.
- Benefit name.

---

Example:

Search:

FOX HOME

Results:

- FOX HOME Voucher.
- BUYME redeemable at FOX HOME.
- Hever Membership including FOX HOME.

---

# 11. Add Benefit

Entry point:

+ Add Benefit

---

Select type:

- Gift Card.
- Voucher.
- Membership.

---

Possible fields:

- Name.
- Type.
- Provider.
- Store(s).
- Amount.
- Expiration date.
- Link.
- Image.
- Notes.

---

# 12. Automatic Detection From Link

When entering a link:

The system attempts to identify:

- Provider.
- Store(s).
- Benefit details.

Example:

BUYME link:

Provider:

BUYME

Stores:

- FOX HOME
- ACE
- IKEA

---

# 13. Edit Benefit

The edit screen is identical to the add screen.

Existing information is pre-filled.

---

# 14. Open Benefit

When opening a benefit:

The system opens directly:

- Link.
- Image.

If both exist:

Link has priority.

---

# 15. Statuses

Future statuses:

ACTIVE

USED

EXPIRED

---

# 16. Future Features

Not included in MVP:

- All Benefits page.
- Used Benefits page.
- Expiration notifications.
- OCR.
- Automatic imports.
- Gift card balance tracking.
- Advanced Provider/Store hierarchy.

---

# 17. MVP Scope

The MVP includes:

✅ Saving Gift Cards  
✅ Saving Vouchers  
✅ Saving Memberships  
✅ Supporting Providers with multiple Stores  
✅ Search by Store / Brand / Provider  
✅ Displaying benefits expiring within 30 days  
✅ Editing benefits  
✅ Opening links and images  
✅ Basic link-based detection  

---

# End of Document