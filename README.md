# Codenalogy Telegram Bot (کدنالوژی)

ساخته‌شده با **n8n** و **Google Sheets** به‌عنوان پایگاه داده.

## قابلیت‌ها
- **عضویت اجباری در کانال:** قبل از استفاده، عضویت کاربر در کانال بررسی می‌شود.
- **مرکز ابزارهای AI:** لیست ابزارها به تفکیک دسته، از روی شیت.
- **AI Hunt:** هر روز یک پرامپت حرفه‌ای و یک ترفند، بر اساس تاریخ.
- **امتیاز و سطح:** سه سطح مبتدی، نقره‌ای (۵۰+) و طلایی (۲۰۰+).
- **دعوت دوستان:** لینک اختصاصی؛ هر دعوت موفق ۵۰ امتیاز (فقط برای کاربر جدید و یک‌بار).
- **فروشگاه امتیاز:** خرید جایزه با امتیاز، ثبت سفارش و اطلاع‌رسانی به ادمین.
- **پشتیبانی:** پیام کاربر به ادمین فوروارد می‌شود و ادمین با Reply جواب می‌دهد.

## معماری
```
Telegram Trigger -> Config -> بررسی عضویت کانال
  |- منو و دکمه‌ها (Switch)
  |- ثبت کاربر و رفرال (Google Sheets)
  |- AI Hunt / Tools / Shop (Google Sheets)
  |- پشتیبانی (فوروارد به ادمین و پاسخ)
```

## ساختار شیت (Google Sheets)
| تب | ستون‌ها |
|---|---|
| Users | telegram_id, username, join_date, points, referral_code, invited_by, membership_verified, last_check_date |
| Tools | name, category, description, url, active |
| AIHunt | date (متن، مثل 2026-11-27), prompt, trick |
| Orders | date, telegram_id, username, item, cost, status |

داده‌ی نمونه‌ی تب‌ها در `data/codenalogy-content.xlsx` است.

## راه‌اندازی
1. در n8n: **Import from File** و انتخاب `workflow/codenalogy-bot.n8n.json`.
2. ساخت ربات با @BotFather و ساخت Credential تلگرام در n8n.
3. ساخت Google Sheet با تب‌های بالا و اتصال Credential گوگل.
4. جایگزینی مقدارها در ورک‌فلو: `YOUR_SHEET_ID`، `YOUR_CHANNEL_ID`، `YOUR_INVITE_LINK` و `admin_id` در نود Config.
5. ذخیره و فعال‌سازی ورک‌فلو.

## نکته‌ی امنیتی
توکن ربات و اعتبارنامه‌ها داخل این مخزن نیست و نباید commit شود.

## ابزارها
n8n, Telegram Bot API, Google Sheets
