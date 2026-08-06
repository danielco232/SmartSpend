# SmartSpend - Database Specification

Version: 0.1

---

# 1. Document Purpose

This document defines the database structure of the SmartSpend system.

Its purpose is to describe:

- Which entities exist in the system.
- Which information is stored for each entity.
- The relationships between entities.
- Future requirements that the data model should support.

This document does not define a specific implementation technology and is independent of the choice between SQL, NoSQL, Firebase, or another solution.

---

# 2. Design Principles

## Flexible Data Model

The system must support multiple benefit types:

- Gift Cards
- Vouchers
- Memberships
- Consumer club benefits

---

## Provider First Approach

The system does not assume that every benefit belongs to a single store.

Example:

BUYME:

Provider:
BUYME

Stores:
- FOX HOME
- ACE
- IKEA

Therefore, a separate relationship is maintained between:

Benefit

and:

Store

---

## Many-to-Many Relationships

The system supports many-to-many relationships:

- One benefit can be valid in multiple stores.
- One store can support multiple benefits.

---

# 3. Core Entities

The main entities are:

- User
- Benefit
- Provider
- Store
- BenefitStore
- ProviderStore

---

# 4. User Entity

## Description

Represents a user in the system.

## Fields

- id
- name
- created_at
- updated_at

---

# 5. Benefit Entity

## Description

The main entity representing a benefit owned by a user.

Examples:

- Gift Card
- Voucher
- Membership

## Fields

- id
- user_id
- provider_id
- type
- name
- amount
- expiration_date
- link
- image
- notes
- status
- created_at
- updated_at

## Benefit Types

Possible values:

- GIFT_CARD
- VOUCHER
- MEMBERSHIP

## Benefit Status

Possible values:

- ACTIVE
- USED
- EXPIRED

---

# 6. Provider Entity

## Description

Represents an organization that provides or manages benefits.

Examples:

- BUYME
- Hever
- Consumer club
- Employer

## Fields

- id
- name
- type
- website
- created_at
- updated_at

---

# 7. Store Entity

## Description

Represents a place where a benefit can be redeemed.

Examples:

- FOX HOME
- ACE
- IKEA
- KSP

## Fields

- id
- name
- category
- website
- created_at
- updated_at

---

# 8. BenefitStore Entity

## Description

A relationship entity between benefits and redemption locations.

Required because of the many-to-many relationship.

## Fields

- id
- benefit_id
- store_id
- conditions
- created_at

## Example

BUYME Gift Card:

- FOX HOME
- ACE
- IKEA

---

# 9. ProviderStore Entity

## Description

A relationship between a provider and redemption locations.

Mainly used for general memberships and consumer benefits.

## Example

Hever:

- FOX HOME
- KSP
- Restaurants

## Fields

- id
- provider_id
- store_id
- conditions
- created_at

---

# 10. Relationships

## User → Benefit

One user can have multiple benefits.

---

## Provider → Benefit

One provider can provide multiple benefits.

---

## Benefit ↔ Store

Many-to-many relationship through:

BenefitStore

---

## Provider ↔ Store

Many-to-many relationship through:

ProviderStore

---

# 11. Search Requirements

The system must support searching by:

## Benefit

- name

## Provider

- name

## Store

- name

## Brand

- name

---

# 12. Search Indexes

Recommended indexes:

- Benefit.name
- Provider.name
- Store.name

Purpose:

Support fast search operations.

---

# 13. Expiration Queries

Finding benefits that expire soon:

status = ACTIVE

AND

expiration_date <= today + 30 days

Sorting:

expiration_date ASC

---

# 14. Future Support

The data model should support future capabilities:

## Automatic Imports

Importing benefits from external sources.

---

## OCR

Extracting information from images:

- Amount
- Expiration date
- Provider

---

## Balance Tracking

Tracking remaining balance:

Gift Card:

Initial Amount:
500 ILS

Current Balance:
250 ILS

---

## Notifications

Notifications for:

- Benefits approaching expiration.
- Unused benefits.

---

# 15. Summary

The database model is based on:

- Separation between Provider and Store.
- Many-to-many relationship support.
- Flexible data storage.
- Future scalability.

Main model:

User

↓

Benefits

↓

Provider

↓

Stores

---

# End of Document