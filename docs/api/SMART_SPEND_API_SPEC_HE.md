# מפרט API - SmartSpend

**מזהה מסמך:** SP-API-001
**גרסה:** 0.1
**סטטוס:** טיוטה (Draft)
**טכנולוגיה:** בלתי תלויה (Technology Agnostic)

---

# 1. סקירה כללית (Overview)

## 1.1 מטרה

ממשק ה־API של SmartSpend מספק שירותי Backend לניהול, ארגון ושליפה של הטבות אישיות, קופונים, תווי קנייה ומידע הקשור לבתי עסק וספקים.

גרסת ה־MVP מיועדת למשתמשת יחידה, תוך שמירה על מבנה שניתן להרחבה עתידית למספר משתמשים.

## 1.2 תחום אחריות

ה־API תומך ביכולות הבאות:

* ניהול הטבות
* מעקב אחר תאריכי תפוגה
* ניהול ספקים ובתי עסק
* חיפוש הטבות זמינות
* אספקת מידע עבור מסך הבית באפליקציה

---

# 2. עקרונות API

## 2.1 עקרונות תכנון

ה־API מבוסס על העקרונות הבאים:

* ארכיטקטורה מבוססת משאבים (Resource-Oriented Architecture)
* הפרדה ברורה בין Frontend ל־Backend
* יכולת הרחבה עתידית
* מינימום מורכבות עבור MVP
* מבנה תגובות עקבי

---

# 3. אימות והרשאות (Authentication & Access Control)

## 3.1 אימות בגרסת MVP

בגרסת ה־MVP המערכת פועלת במצב של משתמשת יחידה.

בגרסה הראשונה אין צורך במנגנון Authentication.

הארכיטקטורה צריכה לאפשר הוספת Authentication בגרסאות עתידיות.

---

# 4. משאבי מערכת (Resources)

משאבי ה־API המרכזיים:

| משאב       | תיאור                                      |
| ---------- | ------------------------------------------ |
| Benefits   | הטבות, תווי קנייה וקופונים השייכים למשתמשת |
| Providers  | ארגונים או חברות המנפיקים הטבות            |
| Stores     | בתי עסק בהם ניתן לממש הטבות                |
| Categories | סיווג סוגי הטבות                           |
| Dashboard  | מידע מרוכז עבור מסך הבית                   |
| Search     | חיפוש הטבות ובתי עסק                       |

---

# 5. נקודות קצה (Endpoints)

## 5.1 הטבות (Benefits)

### קבלת כל ההטבות

```http
GET /api/v1/benefits
```

מחזיר את כל ההטבות השמורות במערכת.

---

### קבלת הטבה לפי מזהה

```http
GET /api/v1/benefits/{benefitId}
```

---

### יצירת הטבה חדשה

```http
POST /api/v1/benefits
```

דוגמת Request:

```json
{
  "name": "Example Gift Card",
  "providerId": "provider_001",
  "value": 250,
  "expirationDate": "2026-12-31",
  "categoryId": "shopping"
}
```

---

### עדכון הטבה

```http
PATCH /api/v1/benefits/{benefitId}
```

---

### מחיקת הטבה

```http
DELETE /api/v1/benefits/{benefitId}
```

---

### קבלת הטבות שעומדות לפוג

```http
GET /api/v1/benefits/expiring
```

פרמטרים:

| פרמטר | תיאור                   |
| ----- | ----------------------- |
| days  | מספר הימים קדימה לבדיקה |

דוגמה:

```http
GET /api/v1/benefits/expiring?days=30
```

מחזיר הטבות ממוינות לפי תאריך התפוגה הקרוב ביותר.

---

## 5.2 ספקים (Providers)

### קבלת כל הספקים

```http
GET /api/v1/providers
```

---

### קבלת ספק לפי מזהה

```http
GET /api/v1/providers/{providerId}
```

---

## 5.3 בתי עסק (Stores)

### קבלת כל בתי העסק

```http
GET /api/v1/stores
```

---

### קבלת בתי עסק לפי ספק

```http
GET /api/v1/providers/{providerId}/stores
```

---

## 5.4 קטגוריות (Categories)

### קבלת קטגוריות

```http
GET /api/v1/categories
```

---

## 5.5 חיפוש (Search)

### חיפוש הטבות ובתי עסק

```http
GET /api/v1/search
```

פרמטרים:

| פרמטר | תיאור       |
| ----- | ----------- |
| query | טקסט לחיפוש |

דוגמה:

```http
GET /api/v1/search?query=Fox
```

החיפוש כולל:

* שמות הטבות
* ספקים
* בתי עסק

---

## 5.6 מסך בית (Dashboard)

### קבלת נתוני Dashboard

```http
GET /api/v1/dashboard
```

מחזיר:

* הטבות שעומדות לפוג בקרוב
* הטבות שנוספו לאחרונה
* סטטיסטיקות סיכום של ההטבות

---

# 6. מודלי מידע (Data Models)

הישויות המרכזיות בהן משתמש ה־API:

* Benefit
* Provider
* Store
* Category

הגדרת השדות המלאה תופיע במסמך Data Model Specification.

---

# 7. טיפול בשגיאות (Error Handling)

ה־API משתמש במבנה אחיד להחזרת שגיאות.

דוגמה:

```json
{
  "error": {
    "code": "RESOURCE_NOT_FOUND",
    "message": "Benefit was not found"
  }
}
```

## 7.1 קודי שגיאה נפוצים

| קוד                | תיאור                |
| ------------------ | -------------------- |
| RESOURCE_NOT_FOUND | המשאב המבוקש לא נמצא |
| INVALID_REQUEST    | נתוני בקשה לא תקינים |
| INTERNAL_ERROR     | שגיאת שרת            |

---

# 8. הרחבות עתידיות (Future Extensions)

יכולות אפשריות לגרסאות עתידיות:

* ניהול משתמשים
* סנכרון בין מספר מכשירים
* יצירת הטבות באמצעות OCR
* ייבוא מאימיילים ו־SMS
* תזכורות אוטומטיות לפני תפוגה
* אינטגרציות מול ספקים חיצוניים

---

# End of Document