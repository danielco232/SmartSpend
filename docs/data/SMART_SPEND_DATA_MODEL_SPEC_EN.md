# SmartSpend Data Model Specification

**Document ID:** SP-DATA-001
**Version:** 0.1
**Status:** Draft
**Technology:** Agnostic

---

# 1. Overview

## 1.1 Purpose

The SmartSpend Data Model Specification defines the core data entities, attributes, and relationships used by the SmartSpend application.

This document serves as the common reference between:

* Database design
* API contracts
* Frontend implementation
* Business logic

## 1.2 Scope

The data model supports:

* Personal benefit management
* Benefit expiration tracking
* Provider and store relationships
* Benefit categorization
* Dashboard data generation

The MVP is designed for a single user while maintaining future scalability.

---

# 2. Data Modeling Principles

The data model follows these principles:

* Clear separation between entities
* Avoiding duplicated information
* Supporting future expansion
* Keeping MVP complexity minimal
* Maintaining consistency across API and Database layers

---

# 3. Entity Overview

The main entities are:

| Entity           | Description                                       |
| ---------------- | ------------------------------------------------- |
| Benefit          | A coupon, gift card, voucher, or personal benefit |
| Provider         | Organization issuing the benefit                  |
| Store            | Business where the benefit can be used            |
| Category         | Classification of benefits                        |
| DashboardSummary | Aggregated data for the application dashboard     |

---

# 4. Entity Definitions

# 4.1 Benefit

## Description

Represents a personal benefit stored by the user.

Examples:

* Gift card
* Discount coupon
* Voucher
* Employee benefit

## Attributes

| Field          | Type     | Required | Description                     |
| -------------- | -------- | -------- | ------------------------------- |
| id             | UUID     | Yes      | Unique benefit identifier       |
| name           | String   | Yes      | Benefit display name            |
| providerId     | UUID     | No       | Related provider identifier     |
| categoryId     | UUID     | No       | Related category identifier     |
| value          | Number   | No       | Monetary value or benefit value |
| currency       | String   | No       | Currency code                   |
| expirationDate | Date     | No       | Benefit expiration date         |
| status         | Enum     | Yes      | Current benefit status          |
| notes          | String   | No       | User notes                      |
| imageUrl       | String   | No       | Image reference                 |
| createdAt      | DateTime | Yes      | Creation timestamp              |
| updatedAt      | DateTime | Yes      | Last update timestamp           |

## Status Values

Possible values:

* ACTIVE
* EXPIRED
* USED
* ARCHIVED

---

# 4.2 Provider

## Description

Represents the organization or company that issued the benefit.

Examples:

* Employer
* Credit card company
* Retail chain
* Service provider

## Attributes

| Field      | Type     | Required | Description                |
| ---------- | -------- | -------- | -------------------------- |
| id         | UUID     | Yes      | Unique provider identifier |
| name       | String   | Yes      | Provider name              |
| logoUrl    | String   | No       | Provider logo              |
| websiteUrl | String   | No       | Provider website           |
| notes      | String   | No       | Additional information     |
| createdAt  | DateTime | Yes      | Creation timestamp         |
| updatedAt  | DateTime | Yes      | Last update timestamp      |

---

# 4.3 Store

## Description

Represents a business where a benefit can be redeemed.

## Attributes

| Field      | Type     | Required | Description                 |
| ---------- | -------- | -------- | --------------------------- |
| id         | UUID     | Yes      | Unique store identifier     |
| name       | String   | Yes      | Store name                  |
| providerId | UUID     | No       | Related provider identifier |
| address    | String   | No       | Store address               |
| websiteUrl | String   | No       | Store website               |
| notes      | String   | No       | Additional information      |
| createdAt  | DateTime | Yes      | Creation timestamp          |
| updatedAt  | DateTime | Yes      | Last update timestamp       |

---

# 4.4 Category

## Description

Represents the classification of a benefit.

Examples:

* Food
* Fashion
* Entertainment
* Home
* Travel

## Attributes

| Field     | Type     | Required | Description                |
| --------- | -------- | -------- | -------------------------- |
| id        | UUID     | Yes      | Unique category identifier |
| name      | String   | Yes      | Category name              |
| icon      | String   | No       | Category icon reference    |
| createdAt | DateTime | Yes      | Creation timestamp         |

---

# 4.5 DashboardSummary

## Description

Represents calculated information displayed on the application home screen.

This entity is generated dynamically and is not necessarily stored permanently.

## Attributes

| Field            | Type    | Required | Description               |
| ---------------- | ------- | -------- | ------------------------- |
| totalBenefits    | Integer | Yes      | Total number of benefits  |
| activeBenefits   | Integer | Yes      | Number of active benefits |
| expiringBenefits | Integer | Yes      | Benefits expiring soon    |
| recentlyAdded    | List    | No       | Recently added benefits   |

---

# 5. Entity Relationships

## Benefit - Provider

Relationship:

```
Provider 1 ---- N Benefit
```

A provider can issue multiple benefits.

A benefit can optionally belong to one provider.

---

## Benefit - Category

Relationship:

```
Category 1 ---- N Benefit
```

A category can contain multiple benefits.

A benefit can optionally belong to one category.

---

## Provider - Store

Relationship:

```
Provider 1 ---- N Store
```

A provider can have multiple associated stores.

---

## Benefit - Store

Future extension:

```
Benefit N ---- N Store
```

A benefit may be usable in multiple stores.

This relationship will be implemented when multi-store redemption logic is required.

---

# 6. Data Validation Rules

Examples:

| Rule            | Description                |
| --------------- | -------------------------- |
| Benefit name    | Must not be empty          |
| Expiration date | Must be a valid date       |
| Value           | Must not be negative       |
| Status          | Must use predefined values |

---

# 7. Future Extensions

Possible future additions:

* Benefit images and attachments
* OCR extracted fields
* Automatic provider detection
* Multiple users
* Benefit sharing
* External integrations
* Redemption history

---

# End of Document
