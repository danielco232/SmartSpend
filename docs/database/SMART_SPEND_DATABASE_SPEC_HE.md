# SmartSpend - מפרט בסיס נתונים

Version: 0.1

---

# 1. מטרת המסמך

מסמך זה מגדיר את מבנה בסיס הנתונים של מערכת SmartSpend.

מטרתו לתאר:

- אילו ישויות קיימות במערכת.
- איזה מידע נשמר עבור כל ישות.
- מה הקשרים בין הישויות.
- אילו צרכים עתידיים המבנה צריך לתמוך.

המסמך אינו מגדיר מימוש טכנולוגי ספציפי ואינו תלוי בבחירה בין SQL, NoSQL, Firebase או פתרון אחר.

---

# 2. עקרונות תכנון

## Flexible Data Model

המערכת צריכה לתמוך במגוון סוגי הטבות:

- Gift Cards
- Vouchers
- Memberships
- זכאויות ממועדוני צרכנות

---

## Provider First Approach

המערכת אינה מניחה שכל הטבה שייכת למקום אחד בלבד.

לדוגמה:

BUYME:

Provider:
BUYME

Stores:
- FOX HOME
- ACE
- IKEA

לכן נשמר קשר נפרד בין:

Benefit

לבין:

Store

---

## Many-to-Many Relationships

המערכת תומכת בקשרים רבים־לרבים:

- הטבה אחת יכולה להיות תקפה במספר מקומות.
- מקום אחד יכול לקבל מספר הטבות.

---

# 3. ישויות מרכזיות

הישויות המרכזיות:

- User
- Benefit
- Provider
- Store
- BenefitStore
- ProviderStore

---

# 4. User Entity

מייצג משתמשת במערכת.

שדות:

- id
- name
- created_at
- updated_at

---

# 5. Benefit Entity

ישות מרכזית המייצגת הטבה השייכת למשתמשת.

דוגמאות:

- Gift Card
- Voucher
- Membership

שדות:

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

סוגים:

- GIFT_CARD
- VOUCHER
- MEMBERSHIP

סטטוסים:

- ACTIVE
- USED
- EXPIRED

---

# 6. Provider Entity

מייצג גוף שמספק או מנהל הטבות.

דוגמאות:

- BUYME
- חבר
- מועדון צרכנות
- מקום עבודה

שדות:

- id
- name
- type
- website
- created_at
- updated_at

---

# 7. Store Entity

מייצג מקום שבו ניתן לממש הטבה.

דוגמאות:

- FOX HOME
- ACE
- IKEA
- KSP

שדות:

- id
- name
- category
- website
- created_at
- updated_at

---

# 8. BenefitStore Entity

טבלת קשר בין הטבות לבין מקומות מימוש.

נדרשת בגלל קשר רבים־לרבים.

שדות:

- id
- benefit_id
- store_id
- conditions
- created_at

דוגמה:

BUYME Gift Card:

- FOX HOME
- ACE
- IKEA

---

# 9. ProviderStore Entity

קשר בין ספק לבין מקומות מימוש.

משמש בעיקר עבור זכאויות כלליות.

דוגמה:

חבר:

- FOX HOME
- KSP
- מסעדות

שדות:

- id
- provider_id
- store_id
- conditions
- created_at

---

# 10. Relationships

## User → Benefit

משתמשת אחת יכולה להחזיק מספר הטבות.

---

## Provider → Benefit

Provider אחד יכול לספק מספר הטבות.

---

## Benefit ↔ Store

קשר רבים־לרבים באמצעות:

BenefitStore

---

## Provider ↔ Store

קשר רבים־לרבים באמצעות:

ProviderStore

---

# 11. Search Requirements

המערכת תומכת בחיפוש לפי:

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

מומלץ ליצור אינדקסים עבור:

- Benefit.name
- Provider.name
- Store.name

כדי לתמוך בחיפוש מהיר.

---

# 13. Expiration Queries

מציאת הטבות שפגות בקרוב:

status = ACTIVE

AND

expiration_date <= today + 30 days

מיון:

expiration_date ASC

---

# 14. Future Support

תמיכה עתידית:

## Automatic Imports

ייבוא הטבות ממקורות חיצוניים.

## OCR

זיהוי:

- סכום.
- תאריך תפוגה.
- ספק.

## Balance Tracking

מעקב יתרה:

Gift Card:

Initial Amount:
500 ₪

Current Balance:
250 ₪

## Notifications

התראות עבור:

- הטבה שעומדת לפוג.
- הטבה שלא נוצלה.

---

# 15. Summary

מבנה בסיס הנתונים מבוסס על:

- הפרדת Provider מ־Store.
- תמיכה בקשרים רבים־לרבים.
- שמירת מידע גמישה.
- יכולת הרחבה עתידית.

מודל מרכזי:

User

↓

Benefits

↓

Provider

↓

Stores

---

# סוף מסמך