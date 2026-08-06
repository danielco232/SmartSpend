# SmartSpend - UI/UX Specification

Version: 0.4

---

# 1. Document Purpose

This document defines the User Interface (UI) and User Experience (UX) structure of the SmartSpend system.

The document describes:

- Screen structure.
- User flows.
- Component behavior.
- System states.
- Design principles.

This document complements:

SMART_SPEND_PRODUCT_SPEC_EN.md

---

# 2. Core UX Principles

## Search First

SmartSpend is a personal system for managing benefits, vouchers, and eligibility rights.

The main goal:

Allow the user to quickly answer:

"Do I have something I can use at the place where I am?"

Therefore, search focuses mainly on:

- Store.
- Brand.
- Provider.

---

## Mobile First

The system is designed for mobile usage.

Focus:

- Android devices.
- Samsung Galaxy devices.
- One-handed usage.
- Minimal typing.

---

## Simplicity

The system is designed for personal and fast usage.

No need for:

- Registration screen.
- User tutorial.
- Onboarding process.

---

# 3. MVP Navigation Structure

The MVP does not include Bottom Navigation.

The system is based around a central Home Screen.

Structure:

Home Screen

├── Search

│     └── Search Results

│            └── Benefit Details

│

├── Add Benefit

│     └── Select Type

│            └── Add Form

│

└── Expiring Soon Benefits

      └── Benefit Details

---

# 4. Home Screen

## Purpose

The Home Screen is the main entry point of the system.

---

## Structure

Component order:

1. Search bar.
2. Expiring benefits section.
3. Add benefit button.

---

## Empty State

There is no separate screen for a new user or a user with no benefits.

The structure remains identical.

Only the content changes.

---

# 5. Expiring Soon Benefits Section

## Rules

Displays benefits that expire within 30 days.

Benefits are:

- Sorted by closest expiration date.
- Displayed in a horizontal carousel.
- Displayed with a counter.

Format:

<Current>/<Total>

Example:

<1/4>

---

## Expiration Color Rule

More than 10 days remaining:

Normal text.

10 days or fewer remaining:

The remaining days text is displayed in red.

Only the text changes color.

The entire card does not change color.

---

## No Expiring Benefits State

Display:

"No benefits expire within the next 30 days."

---

# 6. Search

## Purpose

Allow users to find benefits by redemption location or benefit source.

---

## Search Types

Search supports:

- Store.
- Brand.
- Provider.
- Benefit name.

---

## Examples

Search:

FOX HOME

Results:

- FOX HOME Voucher.
- BUYME redeemable at FOX HOME.
- Hever Membership including FOX HOME.

---

Search:

Hever

Results:

- Hever Membership.
- Vouchers purchased through Hever.

---

# 7. Search Results Screen

Results are displayed according to relevance.

Priority order:

1. Direct redemption location match.
2. Benefit linked to a location through Provider.
3. Provider match.

---

# 8. Benefit Details Screen

## Purpose

Display all information required to use the benefit.

---

## Displayed Information

- Benefit name.
- Benefit type.
- Provider.
- Store(s).
- Amount or usage conditions.
- Expiration date.
- Link.
- Image.
- Notes.

---

# 9. Provider vs Store

## Provider

A Provider is the organization that supplies or manages a benefit or eligibility right.

Examples:

- BUYME.
- Hever.
- Consumer clubs.

A Provider can be connected to:

- Multiple benefits.
- Multiple Stores.

---

## Store

A Store is the location where a benefit can be redeemed.

Examples:

- FOX HOME.
- ACE.
- IKEA.
- KSP.

---

# 10. Benefit Card

Benefit cards appear in:

- Home Screen.
- Search Results.
- Future All Benefits page.

---

## Card Information

Displays:

- Name.
- Type.
- Amount/discount.
- Expiration.
- Redemption location.

---

## Title Hierarchy

When there is one main Store:

The Store name is displayed as the title.

Example:

FOX HOME

BUYME

250 ₪

---

When there are multiple Stores:

The Provider name is displayed as the title.

Example:

BUYME

250 ₪

Available at:

FOX HOME +12

---

When the benefit is a Membership:

The Provider is displayed as the title.

Example:

Hever

Hever Benefits

Available at 100+ stores

---

# 11. Add Benefit

## Entry Point

[+ Add Benefit]

---

## Select Benefit Type

Options:

- Gift Card.
- Voucher.
- Membership.

---

## Form

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

# 12. Link-Based Detection

When adding a link:

The system attempts to identify:

- Provider.
- Store(s).
- Benefit details.

Example:

BUYME link:

Provider:

BUYME

Stores:

FOX HOME  
ACE  
IKEA

---

If detection fails:

The user can continue manually.

---

# 13. Edit Benefit

The edit screen is identical to the add screen.

Existing information is already populated.

---

Flow:

Benefit Details

↓

Edit

↓

Filled Form

↓

Save

↓

Return to Details

---

# 14. Open Benefit Action

When pressing:

[Open Benefit]

The system opens directly.

No confirmation screen.

---

Priority:

1. Link.
2. Image.

---

# 15. Missing Information

Saving is never blocked.

Missing information is displayed as:

"Unknown"

---

# 16. System Messages

## Success

✓ Benefit saved

✓ Changes saved

---

## Delete

"Delete this benefit?"

Options:

[Cancel]

[Delete]

---

# 17. Future Features

Not included in MVP:

- All Benefits page.
- Used Benefits page.
- Expiration notifications.
- WhatsApp reminders.
- OCR.
- Automatic imports.
- Advanced Provider/Store hierarchy.
- Gift card balance tracking.

---

# 18. Used Benefits (Future)

A future page will display used benefits.

Statuses:

ACTIVE

USED

EXPIRED

---

When a gift card reaches zero balance:

It will automatically move to Used Benefits.

---

# 19. MVP Scope

The MVP includes:

✅ Adding Gift Cards  
✅ Adding Vouchers  
✅ Adding Memberships  
✅ Supporting Providers with multiple Stores  
✅ Search by Store / Brand / Provider  
✅ Displaying benefits expiring within 30 days  
✅ Sorting by expiration date  
✅ Editing benefits  
✅ Opening links and images  
✅ Basic link-based detection  

---

# End of Document