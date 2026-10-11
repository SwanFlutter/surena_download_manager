<div align="center">

<img src="assets/logo/logo_splash.png" alt="surena_download_manager logo" width="180"/>

# SurenaDownloadManager

**A modern, glassmorphism-style download manager for desktop — built with Flutter.**

`Tech repo name: surena_download_manager`

![Flutter](https://img.shields.io/badge/Flutter-3.47-02569B?logo=flutter&logoColor=white)
![Dart](https://img.shields.io/badge/Dart-3.13-0175C2?logo=dart&logoColor=white)
![Platform](https://img.shields.io/badge/Platform-Windows%20%7C%20Linux%20%7C%20macOS-0078D4?logo=windows95&logoColor=white)
![i18n](https://img.shields.io/badge/i18n-English%20%7C%20فارسی-green)

[English](#-english) · [فارسی](#-فارسی)

</div>

---

<a id="-english"></a>
## 🇬🇧 English

### What is SurenaDownloadManager?

**SurenaManager** is a full-featured **desktop download manager** for **Windows** (with
Linux/macOS targets in the repository), written in **Flutter** with the
[`get_x_master`](https://pub.dev/packages/get_x_master) state-management stack.
The UI is a hand-crafted glassmorphism design rebuilt from Stitch mockups, with a
fully bilingual interface (**English / فارسی**) and a dynamic accent-color system.

Unlike a mock prototype, SurenaManager ships a **real download engine**: multi-segment
HTTP downloads with resume support, queue execution, disk-space guarding, clipboard
link capture, and OS integration (tray, open/reveal file, shutdown after completion).
A built-in **Demo Mode** lets you explore the entire UI with simulated traffic.

### ✨ Features

- **Real multi-segment downloads** — HTTP Range requests, pause/resume, retry,
  per-segment progress map, speed limiting, and disk-space guard (`download_engine`)
- **Persistence & crash recovery** — atomic task journal (JSON) + `.part` file
  recovery after restart (`download_persistence`)
- **Queues** — prioritized queues with drag & drop ordering, global concurrency
  and bandwidth control (`queue_scheduler`)
- **Scheduler** — one-shot and recurring scheduled tasks
- **Categories** — automatic categorization of downloads by file type
- **Dashboard** — live throughput chart, global stats, recent activity
- **Clipboard monitoring** — copies a download URL anywhere → the New Download
  dialog opens pre-filled (IDM-style, no browser extension required)
- **Browser extensions** — companion extensions for **Chrome, Edge and Firefox**
  that intercept downloads and hand them to SurenaManager
- **System integration** — system tray, open/reveal files in Explorer, disk
  volume monitoring, optional shutdown after downloads finish (`system_integrator`)
- **Network insights** — real network interface cards and throughput (FFI, `net_tools`)
- **Theming** — light / dark / system theme × 5 dynamic accent colors, glass cards,
  smooth windows-style desktop shell
- **Bilingual UI** — complete English & Persian translations, switchable in-app

### 🧩 Demo Mode vs Real Mode

The engine has two modes, controlled from *Settings → Advanced → Demo Mode*:

| | 🎮 Demo Mode (default) | ⚙️ Real Mode |
|---|---|---|
| Downloads | Simulated (timer-driven, random speeds) | Real HTTP, multi-segment, resumable |
| Persistence | Session only | Tasks + `.part` files survive restart |
| Disk / network cards | Simulated | Real system data |
| Purpose | UI exploration & demos | Everyday downloading |

### 🏗️ Architecture in one line

**The engine acts as the server.** A single permanent `DownloadEngineService`
(`GetxService`) is the *single source of truth* for all data — controllers only
read from it and call its mutators; no parallel state in the UI layer. The real
engine (`download_engine` package) sits behind the same interface, so the UI
never knows the difference. Full map: [`AI_CONTEXT.md`](AI_CONTEXT.md).

### 🌐 Browser Extensions

Load the unpacked extension for your browser from `chrome://extensions`
(Developer mode → *Load unpacked*):

- `SDM_Extension/` — Chrome / Chromium
- `SDM_Extension_Edge/` — Microsoft Edge
- `SDM_Extension_Firefox/` — Firefox

### 🚀 Getting Started

**Prerequisites:** Flutter SDK 3.47+ (Dart 3.13+), Windows 10/11 with Visual
Studio Desktop workload.

> ℹ️ The download stack (`download_engine`, `download_persistence`,
> `queue_scheduler`, `system_integrator`, `clipboard_monitor`, `net_tools`) is
> developed as **companion local packages** and referenced via `path:` in
> `pubspec.yaml` — clone them from the same owner, or point the paths to your copies.

```bash
flutter pub get
flutter run -d windows          # development
flutter build windows --release # release build
```

Or use the one-shot script: **`build_windows.bat`**.
The debug binary lands in `build/windows/x64/runner/Debug/`.

**Login:** the app uses a local session store — any valid e-mail plus a password
of at least 8 characters signs you in (e.g. `you@example.com` / `Password123`).

### 🗺️ Roadmap

- Wire `queue_scheduler.TaskScheduler` into the Scheduler UI
- OS-level notifications (tray is ready via `system_integrator`)
- Full multi-OS parity hardening (Linux / macOS)
- Cloud Sync, Automation and Storage sections (currently "coming soon" in the shell)

### 📚 Documentation

| File | Contents |
|---|---|
| [`AI_CONTEXT.md`](AI_CONTEXT.md) | Complete architecture map for humans and AIs |
| [`PACKAGE_PROMPTS.md`](PACKAGE_PROMPTS.md) | Build prompts & integration blueprint for the 6 companion packages |
| [`AGENT.md`](AGENT.md) | Mandatory coding rules |
| [`README_NATIVE_MIGRATION.md`](README_NATIVE_MIGRATION.md) | Notes on native (non-Flutter) migration |

### 📄 License

Proprietary — free 30-day trial, Pro by annual subscription.
All rights reserved © SurenaManager team.

---

<a id="-فارسی"></a>
## 🇮🇷 فارسی

<div dir="rtl">

### سورنا منیجر چیست؟

**سورنا‌منیجر** یک **دانلود منیجر دسکتاپیِ کامل** برای **ویندوز** (به‌همراه اهداف
لینوکس و مک در همین مخزن) است که با **فلاتر** و استک مدیریت وضعیت
`get_x_master` ساخته شده است. رابط کاربری یک طراحی شیشه‌ای (Glassmorphism) است
که از ماک‌آپ‌های Stitch بازسازی شده؛ کاملاً **دوزبانه (فارسی / English)** است و
سیستم رنگ اکسنتِ پویا دارد.

برخلاف یک نمونه‌ی ماک، سورنا‌منیجر یک **موتور دانلود واقعی** دارد: دانلود
چندسگمنتی HTTP با قابلیت Resume، اجرای صف‌ها، گارد فضای دیسک، گرفتن لینک از
کلیپ‌بورد و یکپارچگی با سیستم‌عامل (تری، باز کردن فایل، خاموشی پس از اتمام
دانلود). همچنین یک **حالت دمو** داخلی دارد که با ترافیک شبیه‌سازی‌شده کل
رابط کاربری را قابل گشت‌وگذار می‌کند.

### ✨ قابلیت‌ها

- **دانلود واقعی چندسگمنتی** — درخواست‌های HTTP Range، توقف/ادامه، تلاش مجدد،
  نقشه پیشرفت هر سگمنت، محدودسازی سرعت و گارد فضای دیسک (`download_engine`)
- **ماندگاری و بازیابی** — ژورنال اتمیک وظایف (JSON) + بازیابی فایل‌های `.part`
  بعد از ری‌استارت (`download_persistence`)
- **صف‌ها** — صف‌های اولویت‌دار با جابه‌جایی Drag & Drop، هم‌زمانی سراسری و
  کنترل پهنای باند (`queue_scheduler`)
- **زمان‌بند** — وظایف زمان‌بندی‌شده‌ی یک‌باره و تکرارشونده
- **دسته‌بندی‌ها** — دسته‌بندی خودکار دانلودها بر اساس نوع فایل
- **داشبورد** — نمودار زنده throughput، آمار سراسری، فعالیت‌های اخیر
- **نظارت کلیپ‌بورد** — کپی کردن لینک دانلود در هرجای ویندوز ← باز شدن خودکار
  پنجره «دانلود جدید» با URL پیش‌پر (مثل IDM، بدون نیاز به اکستنشن)
- **اکستنشن مرورگر** — اکستنشن‌های همراه برای **کروم، اج و فایرفاکس** که
  دانلودها را رهگیری کرده و به سورنا‌منیجر می‌سپارند
- **یکپارچگی سیستمی** — تری سیستم‌عامل، باز کردن/نمایش فایل در اکسپلورر،
  مانیتورینگ حجم دیسک، خاموشی اختیاری پس از اتمام دانلودها (`system_integrator`)
- **بینش شبکه** — کارت‌های شبکه واقعی و throughput (با FFI، پکیج `net_tools`)
- **تم** — تم روشن / تیره / سیستم × ۵ رنگ اکسنت پویا، کارت‌های شیشه‌ای، پوسته
  دسکتاپی روان
- **رابط دوزبانه** — ترجمه کامل فارسی و انگلیسی، قابل تغییر داخل اپ

### 🧩 حالت دمو یا حالت واقعی؟

موتور دو حالت دارد که از *تنظیمات ← Advanced ← Demo Mode* کنترل می‌شود:

| | 🎮 حالت دمو (پیش‌فرض) | ⚙️ حالت واقعی |
|---|---|---|
| دانلودها | شبیه‌سازی‌شده (تایمری، سرعت تصادفی) | HTTP واقعی، چندسگمنتی، قابل Resume |
| ماندگاری | فقط در همین نشست | وظایف و فایل‌های `.part` بعد از ری‌استارت باقی می‌مانند |
| دیسک / کارت شبکه | شبیه‌سازی‌شده | داده‌های واقعی سیستم |
| هدف | گشت‌وگذار در UI و دمو | دانلود روزمره |

### 🏗️ معماری در یک خط

**موتور، نقش سرور را بازی می‌کند.** یک سرویس دائمی `DownloadEngineService`
(از نوع `GetxService`) تنها «منبع حقیقت» همه داده‌هاست — کنترلرها فقط از آن
می‌خوانند و متدهای تغییردهنده‌اش را صدا می‌زنند؛ در لایه UI هیچ state موازی‌ای
وجود ندارد. موتور واقعی (پکیج `download_engine`) پشت همین اینترفیس می‌نشیند،
بنابراین UI تفاوتی بین دمو و واقعی حس نمی‌کند. نقشه کامل: [`AI_CONTEXT.md`](AI_CONTEXT.md).

### 🌐 اکستنشن‌های مرورگر

اکستنشن مخصوص مرورگر خود را از `chrome://extensions` (Developer mode ←
Load unpacked) نصب کنید:

- `SDM_Extension/` — کروم / کرومیوم
- `SDM_Extension_Edge/` — مایکروسافت اج
- `SDM_Extension_Firefox/` — فایرفاکس

### 🚀 شروع سریع

**پیش‌نیازها:** فلاتر ۳.۴۷ به بالا (دارت ۳.۱۳+)، ویندوز ۱۰/۱۱ با ورک‌لود
Visual Studio Desktop.

> ℹ️ استک دانلود (`download_engine`، `download_persistence`، `queue_scheduler`،
> `system_integrator`، `clipboard_monitor`، `net_tools`) به‌صورت **پکیج‌های
> محلیِ همراه** توسعه یافته و در `pubspec.yaml` با `path:` معرفی شده‌اند —
> آن‌ها را از همان مالک کلون کنید یا مسیرها را به نسخه‌های خودتان تغییر دهید.

```bash
flutter pub get
flutter run -d windows          # توسعه
flutter build windows --release # بیلد نهایی
```

یا از اسکریپت آماده **`build_windows.bat`** استفاده کنید.
باینری دیباگ در `build/windows/x64/runner/Debug/` قرار می‌گیرد.

**ورود:** اپ از مخزن نشست محلی استفاده می‌کند — هر ایمیل معتبر به‌همراه رمز
حداقل ۸ کاراکتری وارد می‌شوید (مثلاً `you@example.com` / `Password123`).

### 🗺️ نقشه راه

- اتصال `queue_scheduler.TaskScheduler` به رابط کاربری زمان‌بند
- اعلان‌های سطح سیستم‌عامل (تری از طریق `system_integrator` آماده است)
- تکمیل هم‌ارزی چندسیستمی (لینوکس / مک)
- بخش‌های Cloud Sync، Automation و Storage (فعلاً «به‌زودی» در پوسته)

### 📚 مستندات

| فایل | محتوا |
|---|---|
| [`AI_CONTEXT.md`](AI_CONTEXT.md) | نقشه کامل معماری برای انسان‌ها و هوش مصنوعی‌ها |
| [`PACKAGE_PROMPTS.md`](PACKAGE_PROMPTS.md) | پرامپت‌های ساخت و نقشه یکپارچه‌سازی ۶ پکیج همراه |
| [`AGENT.md`](AGENT.md) | قوانین اجباری کدنویسی |
| [`README_NATIVE_MIGRATION.md`](README_NATIVE_MIGRATION.md) | یادداشت‌های مهاجرت نیتیو (خارج از فلاتر) |

### 📄 لایسنس

نرم‌افزار اختصاصی — ۳۰ روز دوره آزمایشی رایگان، نسخه Pro با اشتراک سالانه.
تمام حقوق محفوظ است © تیم سورنا‌منیجر.

</div>
