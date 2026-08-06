# SmartSpend - מפרט טכני

Version: 0.1

---

# 1. מטרת המסמך

מסמך זה מגדיר את המבנה הטכני של מערכת SmartSpend.

מטרתו לתרגם את החלטות המוצר וה־UI למבנה שניתן לממש בפיתוח.

מבוסס על:

- SMART_SPEND_PRODUCT_SPEC_HE.md Version 0.4
- SMART_SPEND_UI_SPEC_HE.md Version 0.4

---

# 2. עקרונות טכניים

## MVP First

המערכת תיבנה בצורה המאפשרת:

- פיתוח מהיר.
- הרחבה עתידית.
- מודל נתונים גמיש.

## Data Driven

המערכת מבוססת על ניהול מידע:

- הטבות.
- ספקים.
- מקומות מימוש.
- קשרים ביניהם.

---

# 3. ישויות מרכזיות

## User

מייצג משתמשת.

שדות:

- id
- name
- created_at
- updated_at

---

## Benefit

מייצג הטבה.

סוגים:

- Gift Card
- Voucher
- Membership

שדות:

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

---

## Provider

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

Provider יכול להיות מקושר למספר:

- Benefits
- Stores

---

## Store

מייצג מקום מימוש.

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

---

## BenefitStore

קשר רבים־לרבים בין הטבה למקום מימוש.

שדות:

- id
- benefit_id
- store_id

נדרש עבור מקרים כגון:

BUYME → FOX HOME + ACE + IKEA

---

## ProviderStore

קשר בין ספק לבין מקומות מימוש.

מאפשר זכאויות כלליות.

דוגמה:

חבר → FOX HOME, KSP, מסעדות

שדות:

- id
- provider_id
- store_id
- conditions

---

# 4. לוגיקת חיפוש

החיפוש מתבצע לפי:

- שם הטבה.
- שם Store.
- שם Provider.
- Brand.

סדר עדיפות:

1. התאמה ישירה למקום מימוש.
2. התאמה דרך Provider.
3. התאמה לפי Provider בלבד.

---

# 5. לוגיקת הטבות שפגות בקרוב

המערכת מציגה הטבות שבהן:

expiration_date <= today + 30 days

ובתנאי:

status = ACTIVE

מיון:

expiration_date ASC

---

# 6. חישוב תפוגה

days_left = expiration_date - current_date

כאשר:

days_left <= 10

התצוגה:

- טקסט התפוגה יוצג באדום.
- הכרטיס עצמו לא ישנה צבע.

---

# 7. מחזור חיים של הטבה

סטטוסים:

- ACTIVE
- USED
- EXPIRED

ב־MVP:

ACTIVE בלבד.

בעתיד:

Gift Card balance = 0

יעביר:

ACTIVE → USED

---

# 8. זיהוי מקישור

Flow:

URL

↓

Provider Detection

↓

Store Detection

↓

Benefit Creation

אם הזיהוי נכשל:

המשתמשת מזינה ידנית.

---

# 9. מידע חלקי

שמירת הטבה אינה נחסמת בגלל מידע חסר.

לדוגמה:

expiration_date = null

תצוגה:

"לא ידוע"

---

# 10. דרישות MVP

חובה:

- User
- Benefit
- Provider
- Store
- BenefitStore relation
- Search
- Expiration logic
- Link storage
- Image storage

---

# 11. הרחבות עתידיות

לא חלק מה־MVP:

- OCR
- ייבוא אוטומטי
- התראות
- תזכורות WhatsApp
- סנכרון יתרת גיפט קארד
- היררכיית Provider מתקדמת
- אינטגרציות מול מועדוני צרכנות

---

# סוף מסמך