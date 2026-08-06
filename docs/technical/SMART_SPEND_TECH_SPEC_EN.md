# SmartSpend - Technical Specification

Version: 0.1

# 1. Document Purpose

This document defines the technical structure of the SmartSpend system.

It translates product and UI decisions into a technical model that can be implemented.

Based on:

- SMART_SPEND_PRODUCT_SPEC_HE.md Version 0.4
- SMART_SPEND_UI_SPEC_HE.md Version 0.4

# 2. Core Technical Principles

## MVP First

The system should support:

- Fast development.
- Future expansion.
- Flexible data model.

## Data Driven

The system is based on managing:

- Benefits.
- Providers.
- Stores.
- Redemption relationships.

# 3. Main Entities

## User

Represents the system user.

Fields:

- id
- name
- created_at
- updated_at

---

## Benefit

Represents:

- Gift Card.
- Voucher.
- Membership.

Fields:

- id
- user_id
- type
- name
- provider_id
- amount
- expiration_date
- link
- image
- notes
- status
- created_at
- updated_at

Benefit types:

- GIFT_CARD
- VOUCHER
- MEMBERSHIP

---

## Provider

Represents an organization that provides or manages benefits or eligibility rights.

Examples:

- BUYME
- Hever
- Consumer clubs
- Workplace benefits

Fields:

- id
- name
- type
- website
- created_at

A Provider can be connected to:

- Multiple Benefits.
- Multiple Stores.

---

## Store

Represents a redemption location.

Examples:

- FOX HOME
- ACE
- IKEA
- KSP

Fields:

- id
- name
- category
- website
- created_at

---

## BenefitStore

Many-to-many relationship between benefits and stores.

Fields:

- id
- benefit_id
- store_id

Required because:

- BUYME can be valid in many stores.
- Memberships can include many stores.

---

## ProviderStore

Represents general provider eligibility.

Example:

Hever → FOX HOME, KSP, Restaurants

Fields:

- id
- provider_id
- store_id
- conditions

# 4. Search Logic

Search fields:

- Benefit name
- Store name
- Provider name
- Brand

Priority:

1. Direct Store match.
2. Benefit connected to Store through Provider.
3. Provider match.

# 5. Expiring Benefits Logic

Show benefits where:

expiration_date <= today + 30 days

and:

status = ACTIVE

Sort:

expiration_date ascending

Expiration warning:

days_left <= 10

Display:

Red expiration text only.

# 6. Benefit Lifecycle

Statuses:

- ACTIVE
- USED
- EXPIRED

MVP:

Only ACTIVE is required.

Future:

Gift card balance reaches zero:

ACTIVE → USED

# 7. Link Detection

Flow:

URL

↓

Provider Detection

↓

Store Detection

↓

Benefit Creation

If detection fails:

Allow manual entry.

# 8. Partial Data

Saving is never blocked.

Missing values are allowed.

Example:

expiration_date = null

Display:

"Unknown"

# 9. MVP Requirements

Required:

- User
- Benefit
- Provider
- Store
- BenefitStore relation
- Search
- Expiration logic
- Link storage
- Image storage

# 10. Future Extensions

Not included in MVP:

- OCR
- Automatic imports
- Notifications
- WhatsApp reminders
- Gift card balance synchronization
- Advanced Provider hierarchy
- External club integrations