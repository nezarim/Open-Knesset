<div dir="rtl" align="right">

# כנסת פתוחה (Open Knesset)

פלטפורמת קוד פתוח להנגשת המידע הפרלמנטרי של הכנסת לציבור הישראלי.
המערכת אוספת, מעבדת ומציגה מידע על חברי כנסת, הצעות חוק, הצבעות, ישיבות ועדות ועוד -- במטרה לקדם שקיפות וחשיבה ביקורתית על תהליכי החקיקה בישראל.

פרויקט של עמותת **הסדנא לידע ציבורי** ([hasadna](https://github.com/hasadna)).

---

## קישורים

<div dir="ltr">

| תיאור | קישור |
|--------|--------|
| קוד מקור (upstream) | https://github.com/hasadna/Open-Knesset |
| תיעוד למפתחים | https://oknesset-devel.readthedocs.org/ |
| תיעוד API | https://oknesset-api.readthedocs.org/ |
| מעקב משימות | https://huboard.com/hasadna/Open-Knesset |

</div>

---

## תכונות

- **חברי כנסת** -- פרופילים, היסטוריית הצבעות, הצעות חוק, נוכחות, סרטונים
- **הצעות חוק ומעקב חקיקה** -- מעקב אחר מחזור החיים של הצעות חוק מהגשה ועד אישור
- **הצבעות** -- תיעוד מלא של הצבעות במליאה, כולל עמדת כל ח"כ
- **ועדות** -- ישיבות ועדות, פרוטוקולים מלאים עם אפשרות הערות טקסט (annotations)
- **סדר יום (אג'נדות)** -- מערכת סדרי יום ציבוריים למעקב אחר נושאים
- **לוביסטים** -- מעקב אחר לוביסטים רשומים ותאגידים
- **פיד פעילות** -- עדכונים על פעולות חברי כנסת בזמן אמת
- **API מלא** -- גישה פרוגרמטית לכל המידע דרך REST API (Tastypie)
- **תגיות ודירוגים** -- מערכת תגיות ציבורית ודירוג תכנים
- **חיפוש** -- חיפוש מלא באמצעות Google Custom Search
- **הזנות RSS** -- פידים להצבעות, הצעות חוק, הערות ופעילות כללית
- **התחברות חברתית** -- כניסה דרך Twitter, Facebook, Google, GitHub

---

## טכנולוגיות

<div dir="ltr">

| רכיב | טכנולוגיה |
|-------|-----------|
| שפה | Python 2 |
| פריימוורק | Django 1.6 |
| מסד נתונים | SQLite (פיתוח) / PostgreSQL (ייצור) |
| API | django-tastypie 0.9 + tastypie-swagger |
| מיגרציות | South 1.0 |
| אימות | python-social-auth (Twitter, Facebook, Google, GitHub) |
| JWT | PyJWT + HS256 |
| שרת | Gunicorn + Apache |
| Cache | Memcached (ייצור) / DummyCache (פיתוח) |
| ניהול Deploy | Fabric |
| בדיקות | django-nose + Selenium |
| CSS | LESS |
| עורך טקסט | TinyMCE |
| Feature Flags | django-waffle |
| CORS | django-cors-headers |
| SSL | django-sslify |

</div>

---

## מבנה הפרויקט

<div dir="ltr">

```
Open-Knesset/
├── knesset/           # הגדרות Django ראשיות (settings, urls, wsgi)
├── mks/               # חברי כנסת ומפלגות
├── laws/              # חוקים, הצעות חוק, הצבעות
├── committees/         # ועדות כנסת ופרוטוקולים
├── plenum/            # ישיבות מליאה
├── agendas/           # סדרי יום ציבוריים
├── lobbyists/         # לוביסטים ותאגידים
├── persons/           # אנשים (לא ח"כים)
├── events/            # אירועים
├── video/             # סרטוני וידאו
├── apis/              # REST API (Tastypie v2)
│   └── resources/     # הגדרת כל ה-API endpoints
├── accounts/          # ניהול חשבונות
├── user/              # פרופיל משתמש
├── auxiliary/          # תשתיות עזר, חיפוש, sitemap
├── simple/            # ניתוח הצעות חוק ממשלתיות
├── mmm/               # מסמכי מרכז מחקר ומידע
├── ok_tag/            # מערכת תגיות
├── tagvotes/          # הצבעות על תגיות
├── suggestions/       # הצעות משתמשים
├── notify/            # התראות
├── links/             # קישורים
├── polyorg/           # ארגונים פוליטיים ורשימות
├── kikar/             # אינטגרציה עם כיכר המדינה
├── okhelptexts/       # טקסטים של עזרה
├── hashnav/           # ניווט בתגיות
├── templates/         # תבניות Django
├── static/            # קבצים סטטיים
├── locale/            # תרגומים (עברית)
├── deploy/            # קבצי deploy (crontab, gunicorn, wsgi)
├── docs/              # תיעוד (Sphinx)
├── data/              # קבצי נתונים
├── media/             # קבצי מדיה שהועלו
├── tests/             # בדיקות
├── manage.py          # Django CLI
├── fabfile.py         # פקודות Fabric ל-deploy
├── requirements.txt   # תלויות Python
└── setup.py           # הגדרת חבילה
```

</div>

---

## התקנה והרצה

### דרישות מוקדמות

- Python 2.7
- pip
- virtualenv (מומלץ)
- Git

### שלבי התקנה

<div dir="ltr">

```bash
# שכפול הפרויקט
git clone https://github.com/hasadna/Open-Knesset.git
cd Open-Knesset

# יצירת סביבה וירטואלית
virtualenv venv
source venv/bin/activate

# התקנת תלויות
pip install -r requirements.txt

# יצירת מסד נתונים
python manage.py syncdb --noinput

# הרצת מיגרציות
python manage.py migrate

# טעינת נתונים ראשוניים
python manage.py loaddata dev.json.gz

# הרצת שרת פיתוח
python manage.py runserver
```

</div>

השרת יהיה זמין בכתובת `http://127.0.0.1:8000/`

### הרצת בדיקות

<div dir="ltr">

```bash
python manage.py test
```

</div>

---

## API

המערכת חושפת REST API מלא בגרסה v2 דרך `django-tastypie`.

### Endpoints זמינים

<div dir="ltr">

| Endpoint | תיאור |
|----------|--------|
| `/api/v2/member/` | חברי כנסת |
| `/api/v2/party/` | מפלגות |
| `/api/v2/bill/` | הצעות חוק |
| `/api/v2/vote/` | הצבעות |
| `/api/v2/vote-action/` | פעולות הצבעה |
| `/api/v2/law/` | חוקים |
| `/api/v2/committee/` | ועדות |
| `/api/v2/committee-meeting/` | ישיבות ועדות |
| `/api/v2/protocol-part/` | חלקי פרוטוקול |
| `/api/v2/agenda/` | סדרי יום |
| `/api/v2/event/` | אירועים |
| `/api/v2/lobbyist/` | לוביסטים |
| `/api/v2/lobbyist-corporation/` | תאגידי לוביסטים |
| `/api/v2/person/` | אנשים |
| `/api/v2/video/` | סרטונים |
| `/api/v2/link/` | קישורים |
| `/api/v2/tag/` | תגיות |

</div>

תיעוד אינטראקטיבי (Swagger) זמין בנתיב `/api/v2/doc/`.

ברירת המחדל: עד 1,000 רשומות לעמוד (`API_LIMIT_PER_PAGE`).

---

## אבטחה

### ממצאים בקוד

- **`SECRET_KEY` חשוף** -- המפתח הסודי של Django מוגדר ישירות בקובץ `knesset/settings.py` ולא דרך משתנה סביבה. בסביבת ייצור יש לדרוס דרך `local_settings.py`.
- **`DEBUG = True` כברירת מחדל** -- יש לוודא שבסביבת ייצור הערך משונה ל-`False` דרך `local_settings.py`.
- **מפתחות Twitter API חשופים** -- מפתחות `SOCIAL_AUTH_TWITTER_KEY` ו-`SOCIAL_AUTH_TWITTER_SECRET` מופיעים ב-settings (מיועדים ל-localhost בלבד).
- **CORS פתוח** -- `CORS_ORIGIN_ALLOW_ALL = True` כברירת מחדל. בסביבת ייצור יש להגביל.
- **Session Serializer** -- שימוש ב-`PickleSerializer` (פחות מאובטח מ-JSON), נדרש עבור python-social-auth.
- **SSL** -- `django-sslify` מותקן אך מושבת כברירת מחדל (`SSLIFY_DISABLE = True`). מופעל בייצור.
- **CSRF Protection** -- middleware מופעל כברירת מחדל.
- **JWT** -- שימוש באלגוריתם HS256 עם תוקף של 48 שעות.
- **`local_settings.py`** -- הקובץ מיובא בסוף settings ומשמש לדריסת הגדרות רגישות. אסור לבצע commit לקובץ זה.

### המלצות

1. אל תשתמשו ב-settings המוגדרים בקוד לסביבת ייצור
2. הגדירו `SECRET_KEY` כמשתנה סביבה
3. הגבילו CORS origins
4. ודאו ש-`DEBUG = False` בייצור
5. השתמשו ב-HTTPS (הפעילו sslify)

---

## משתני סביבה והגדרות

ההגדרות הראשיות נמצאות ב-`knesset/settings.py`.
לדריסת הגדרות בסביבה מקומית או בייצור, יש ליצור קובץ `local_settings.py` בתיקיית `knesset/`:

<div dir="ltr">

```python
# knesset/local_settings.py (לא לבצע commit)

DEBUG = False
TEMPLATE_DEBUG = False

SECRET_KEY = 'your-secret-key-here'

DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql_psycopg2',
        'NAME': 'oknesset',
        'USER': 'oknesset',
        'PASSWORD': '...',
        'HOST': 'localhost',
    }
}

SSLIFY_DISABLE = False
CORS_ORIGIN_ALLOW_ALL = False
CORS_ORIGIN_WHITELIST = ['your-domain.com']

SOCIAL_AUTH_TWITTER_KEY = '...'
SOCIAL_AUTH_TWITTER_SECRET = '...'

CACHES = {
    'default': {
        'BACKEND': 'django.core.cache.backends.memcached.MemcachedCache',
        'LOCATION': '127.0.0.1:11211',
    }
}

YOUTUBE_AUTHSUB_TOKEN = '...'
YOUTUBE_DEVELOPER_KEY = '...'

GOOGLE_MAPS_API_KEY = '...'
```

</div>

### הגדרות מרכזיות

<div dir="ltr">

| הגדרה | ברירת מחדל | תיאור |
|--------|------------|--------|
| `DEBUG` | `True` | מצב פיתוח |
| `SECRET_KEY` | hardcoded | מפתח הצפנה (חובה לשנות בייצור) |
| `DATABASES` | SQLite `dev.db` | מסד נתונים |
| `TIME_ZONE` | `Asia/Jerusalem` | אזור זמן |
| `LANGUAGE_CODE` | `he` | שפת ממשק |
| `SSLIFY_DISABLE` | `True` | השבתת SSL redirect |
| `CORS_ORIGIN_ALLOW_ALL` | `True` | CORS פתוח |
| `API_LIMIT_PER_PAGE` | `1000` | מגבלת תוצאות API |
| `LONG_CACHE_TIME` | `18000` (5 שעות) | זמן cache |
| `JWT_ALGORITHM` | `HS256` | אלגוריתם JWT |
| `JWT_EXPIRATION_DELTA` | 48 שעות | תוקף JWT token |

</div>

---

## רישיון

BSD License -- ראו קובץ [LICENSE](LICENSE).

זכויות יוצרים: Ofri Raviv and others, 2010.

---

## תרומה לפרויקט

הפרויקט מנוהל על ידי [הסדנא לידע ציבורי](https://github.com/hasadna).
לתרומה:

1. בצעו Fork לפרויקט
2. צרו branch חדש לפיצ'ר
3. בצעו commit ו-push
4. פתחו Pull Request

לתיעוד מפורט למפתחים: https://oknesset-devel.readthedocs.org/

</div>
