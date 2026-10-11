<div align="center">

<img width="992" height="992" alt="logo_splash" src="https://github.com/user-attachments/assets/6347583d-5cfd-432a-9c6c-3e7668e6b5a3" />


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



https://github.com/user-attachments/assets/aabb7d44-7b3d-416b-b5b7-61842153b2ad



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

### ⬇️ Download

Grab the latest build from the [**Releases**](https://github.com/SwanFlutter/surena_download_manager/releases/latest) page:

| Platform / Asset | File | Direct link |
|---|---|---|
| 🪟 **Windows app** (v1.0.0) | `SurenaDownloadManager.exe` | [Download](https://github.com/SwanFlutter/surena_download_manager/releases/download/v1.0.0/SurenaDownloadManager.exe) |
| 🌐 **Extension** — Chrome / Chromium / Brave / Opera | `SDM_Extension.zip` | [Download](https://github.com/SwanFlutter/surena_download_manager/releases/download/v1.0.0/SDM_Extension.zip) |
| 🌐 **Extension** — Microsoft Edge | `SDM_Extension_Edge.zip` | [Download](https://github.com/SwanFlutter/surena_download_manager/releases/download/v1.0.0/SDM_Extension_Edge.zip) |
| 🌐 **Extension** — Mozilla Firefox | `SDM_Extension_Firefox.zip` | [Download](https://github.com/SwanFlutter/surena_download_manager/releases/download/v1.0.0/SDM_Extension_Firefox.zip) |

> The app runs on Windows out of the box; Linux & macOS targets live in the source repo.

### 🎬 Promo Video

An interactive product demo (no video file — it plays right in your browser):

- [**English promo**](https://swanflutter.github.io/surena_download_manager/surena_promo_en.html) · [`surena_promo_en.html`](https://github.com/SwanFlutter/surena_download_manager/blob/main/surena_promo_en.html)
- [**Promo فارسی**](https://swanflutter.github.io/surena_download_manager/Surena%20Promo%20Video.html) · [`Surena Promo Video.html`](https://github.com/SwanFlutter/surena_download_manager/blob/main/Surena%20Promo%20Video.html)

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

### 🧩 Browser Extensions — manual install

The companion extensions intercept downloads in your browser and hand them straight to
SurenaManager (IDM-style). Each browser ships as a **zipped, unpacked extension** in the
release — download the one for your browser, then load it manually:

| Browser | Release asset |
|---|---|
| Google Chrome / Chromium / Brave / Opera | `SDM_Extension.zip` |
| Microsoft Edge | `SDM_Extension_Edge.zip` |
| Mozilla Firefox | `SDM_Extension_Firefox.zip` |

<details open>
<summary><b>Chrome / Edge / Chromium / Brave / Opera</b> — Load unpacked</summary>

<br>

1. Download `SDM_Extension.zip` (Chrome-family) or `SDM_Extension_Edge.zip` (Edge) from the [Releases](https://github.com/SwanFlutter/surena_download_manager/releases/latest) page.
2. **Extract** the `.zip` to a permanent folder (right-click → *Extract All…*). Keep the folder — the browser reloads the extension from it on every launch.
3. Open the extensions page in your browser:
   - Chrome / Brave / Opera / Chromium → `chrome://extensions`
   - Microsoft Edge → `edge://extensions`
4. Turn **Developer mode** ON (toggle in the top-right corner).
5. Click **Load unpacked** and select the **extracted `SDM_Extension` folder** — i.e. the folder that *contains* `manifest.json` (not the `.zip`).
6. Pin the extension to the toolbar. SurenaManager must be running for the extension to hand off downloads.

> ✅ Tip: after a SurenaManager update, re-download the extension zip and load it again.

</details>

<details>
<summary><b>Mozilla Firefox</b> — Load temporary add-on</summary>

<br>

1. Download `SDM_Extension_Firefox.zip` from the [Releases](https://github.com/SwanFlutter/surena_download_manager/releases/latest) page.
2. **Extract** the `.zip` to a permanent folder.
3. Open `about:debugging#/runtime/this-firefox` in Firefox.
4. Click **Load Temporary Add-on…** and pick the **`manifest.json`** inside the extracted `SDM_Extension_Firefox` folder.
5. The icon appears in the toolbar. Because Firefox loads *temporary* add-ons, repeat steps 3–4 after each browser restart — or sign & install it permanently through `about:addons`.

</details>


**Login:** the app uses a local session store — any valid e-mail plus a password
of at least 8 characters signs you in (e.g. `you@example.com` / `Password123`).



### 📄 License

Proprietary — free 30-day trial, Pro by annual subscription.
All rights reserved © SwanFlutter.

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

### ⬇️ دانلود

آخرین نسخه را از صفحه‌ی [**Releases**](https://github.com/SwanFlutter/surena_download_manager/releases/latest) دریافت کنید:

| سکو / فایل | نام فایل | لینک مستقیم |
|---|---|---|
| 🪟 **اپ ویندوز** (نسخه ۱.۰.۰) | `SurenaDownloadManager.exe` | [دانلود](https://github.com/SwanFlutter/surena_download_manager/releases/download/v1.0.0/SurenaDownloadManager.exe) |
| 🌐 **اکستنشن** — کروم / کرومیوم / Brave / Opera | `SDM_Extension.zip` | [دانلود](https://github.com/SwanFlutter/surena_download_manager/releases/download/v1.0.0/SDM_Extension.zip) |
| 🌐 **اکستنشن** — مایکروسافت اج | `SDM_Extension_Edge.zip` | [دانلود](https://github.com/SwanFlutter/surena_download_manager/releases/download/v1.0.0/SDM_Extension_Edge.zip) |
| 🌐 **اکستنشن** — فایرفاکس | `SDM_Extension_Firefox.zip` | [دانلود](https://github.com/SwanFlutter/surena_download_manager/releases/download/v1.0.0/SDM_Extension_Firefox.zip) |

> اپ روی ویندوز به‌صورت آماده اجرا می‌شود؛ هدف‌های لینوکس و مک در مخزن سورس قرار دارند.

### 🎬 ویدیوی معرفی (Promo)

دموی تعاملی محصول را ببینید (نیازی به فایل ویدیو نیست — همان‌جا در مرورگر پخش می‌شود):

- [**معرفی فارسی**](https://swanflutter.github.io/surena_download_manager/Surena%20Promo%20Video.html) · [`Surena Promo Video.html`](https://github.com/SwanFlutter/surena_download_manager/blob/main/Surena%20Promo%20Video.html)
- [**English promo**](https://swanflutter.github.io/surena_download_manager/surena_promo_en.html) · [`surena_promo_en.html`](https://github.com/SwanFlutter/surena_download_manager/blob/main/surena_promo_en.html)

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

### 🧩 اکستنشن‌های مرورگر — نصب دستی

اکستنشن همراهِ هر مرورگر، دانلودها را رهگیری کرده و مستقیماً به سورنا‌منیجر می‌سپارد
(مثل IDM). هر مرورگر به‌صورت یک **اکستنشنِ فشرده (zip)** در بخش Releases قرار دارد —
نسخه‌ی مناسب مرورگر خود را دانلود و سپس به‌صورت دستی نصب کنید:

| مرورگر | فایل اکستنشن |
|---|---|
| Google Chrome / کرومیوم / Brave / Opera | `SDM_Extension.zip` |
| Microsoft Edge | `SDM_Extension_Edge.zip` |
| Mozilla Firefox | `SDM_Extension_Firefox.zip` |

<details open>
<summary><b>Chrome / Edge / کرومیوم / Brave / Opera</b> — بارگذاری unpacked</summary>

<br>

1. فایل `SDM_Extension.zip` (خانواده‌ی کروم) یا `SDM_Extension_Edge.zip` (اج) را از صفحه‌ی [Releases](https://github.com/SwanFlutter/surena_download_manager/releases/latest) دانلود کنید.
2. فایل `.zip` را در یک پوشه‌ی دائمی **باز (Extract) کنید** (راست‌کلیک → *Extract All…*). این پوشه را نگه دارید — مرورگر در هر اجرا از آن بارگذاری می‌کند.
3. صفحه‌ی اکستنشن‌ها را در مرورگر باز کنید:
   - Chrome / Brave / Opera / کرومیوم → `chrome://extensions`
   - مایکروسافت اج → `edge://extensions`
4. حالت **Developer mode** (حالت توسعه‌دهنده) را روشن کنید (کلید بالا-راست).
5. روی **Load unpacked** کلیک کنید و **پوشه‌ی باز‌شده‌ی `SDM_Extension`** را انتخاب کنید — یعنی پوشه‌ای که فایل `manifest.json` درون آن است (نه خودِ فایل `.zip`).
6. اکستنشن را به نوار ابزار پین کنید. سورنا‌منیجر باید در حال اجرا باشد تا اکستنشن بتواند دانلودها را به آن بسپارد.

> ✅ نکته: پس از هر به‌روزرسانی سورنا‌منیجر، اکستنشن را دوباره دانلود و بارگذاری کنید.

</details>

<details>
<summary><b>Mozilla Firefox</b> — بارگذاری موقت</summary>

<br>

1. فایل `SDM_Extension_Firefox.zip` را از صفحه‌ی [Releases](https://github.com/SwanFlutter/surena_download_manager/releases/latest) دانلود کنید.
2. فایل `.zip` را در یک پوشه‌ی دائمی **باز (Extract) کنید**.
3. در فایرفاکس، نشانی `about:debugging#/runtime/this-firefox` را باز کنید.
4. روی **Load Temporary Add-on…** کلیک کنید و فایل **`manifest.json`** را از داخل پوشه‌ی باز‌شده‌ی `SDM_Extension_Firefox` انتخاب کنید.
5. آیکون در نوار ابزار ظاهر می‌شود. چون فایرفاکس افزونه‌ها را *موقت* بارگذاری می‌کند، پس از هر بار راه‌اندازی مجدد مرورگر گام‌های ۳ تا ۴ را تکرار کنید — یا از طریق `about:addons` آن را امضا و دائمی نصب کنید.

</details>



**ورود:** اپ از مخزن نشست محلی استفاده می‌کند — هر ایمیل معتبر به‌همراه رمز
حداقل ۸ کاراکتری وارد می‌شوید (مثلاً `you@example.com` / `Password123`).

### 🗺️ نقشه راه

- اتصال `queue_scheduler.TaskScheduler` به رابط کاربری زمان‌بند
- اعلان‌های سطح سیستم‌عامل (تری از طریق `system_integrator` آماده است)
- تکمیل هم‌ارزی چندسیستمی (لینوکس / مک)
- بخش‌های Cloud Sync، Automation و Storage (فعلاً «به‌زودی» در پوسته)

## |

### 📄 لایسنس

نرم‌افزار اختصاصی — ۳۰ روز دوره آزمایشی رایگان، نسخه Pro با اشتراک سالانه.
تمام حقوق محفوظ است © تیم سورنا‌منیجر.

</div>
