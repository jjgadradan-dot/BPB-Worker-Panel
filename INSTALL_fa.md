<h1 align="center">🐶 آموزش نصب پنل DogHub</h1>

<p align="center"><em>راهنمای گام‌به‌گام نصب پنل DogHub روی Cloudflare — رایگان و بدون نیاز به سرور</em></p>

---

## فهرست

1. [پیش‌نیازها](#۱-پیشنیازها)
2. [روش ۱: نصب آنلاین با BPB Wizard (پیشنهادی)](#۲-روش-۱-نصب-آنلاین-با-bpb-wizard-پیشنهادی)
3. [روش ۲: نصب با Wizard در ترمینال (CLI)](#۳-روش-۲-نصب-با-wizard-در-ترمینال-cli)
4. [روش ۳: بیلد نسخه سفارشی (مخصوص توسعه‌دهنده‌ها)](#۴-روش-۳-بیلد-نسخه-سفارشی-مخصوص-توسعهدهندهها)
5. [روش ۴: نصب دستی روی Cloudflare (بدون ویزارد)](#۵-روش-۴-نصب-دستی-روی-cloudflare-بدون-ویزارد)
6. [اولین ورود به پنل](#۶-اولین-ورود-به-پنل)
7. [دریافت کانفیگ‌ها](#۷-دریافت-کانفیگها)
8. [آپدیت و حذف پنل](#۸-آپدیت-و-حذف-پنل)

---

## ۱. پیش‌نیازها

- **یک حساب Cloudflare رایگان** — اگه ندارید [از اینجا ثبت‌نام کنید](https://dash.cloudflare.com/sign-up/) و حتماً ایمیلتون رو تأیید کنید. (لازم نیست دامنه‌ای خریداری کرده باشید)
- برای روش ترمینال: دسترسی به **PowerShell** (ویندوز) یا **Termux** (اندروید) یا ترمینال لینوکس/مک.
- یه برنامه کلاینت مثل **v2rayNG**، **Streisand**، **sing-box** یا **Hiddify** برای استفاده از کانفیگ‌ها.

> 💡 کل فرآیند نصب کمتر از **۲ دقیقه** طول می‌کشه و کاملاً روی حساب رایگان Cloudflare انجام می‌شه.

---

## ۲. روش ۱: نصب آنلاین با BPB Wizard (پیشنهادی)

ساده‌ترین راه نصب، استفاده از [BPB Wizard](https://github.com/bia-pain-bache/BPB-Wizard) نسخه تحت وب هست:

<div dir="ltr">

```url
https://wizard.bpb-panel.workers.dev
```

</div>

### گام ۱: ساخت API Token

1. وارد داشبورد Cloudflare بشید و به مسیر **My Profile → API Tokens** برید (یا از لینکی که خود ویزارد می‌ده).
2. روی **Create Token** کلیک کنید و قالب اختصاصی BPB رو انتخاب کنید.
3. یه اسم دلخواه بدید، توکن رو بسازید و **همون لحظه کپی**ش کنید (فقط یک بار نشون داده می‌شه).

### گام ۲: نصب پنل در ویزارد

1. توکن کپی‌شده رو داخل ویزارد وارد کنید.
2. روش استقرار رو انتخاب کنید:

   | روش | آدرس پنل | توضیح |
   |---|---|---|
   | **Workers** | `panel.<username>.workers.dev/<مسیر>` | پیشنهادی برای شروع |
   | **Pages** | `panel.pages.dev/<مسیر>` | اگه دامنه workers.dev براتون در دسترس نیست |

3. تنظیمات اولیه رو پر کنید (خود ویزارد مقادیر تصادفی پیشنهاد می‌ده):
   - **Panel Password**: پسورد ورود به پنل — یه پسورد قوی بذارید و یادتون بمونه.
   - **Proxy IP path (Secure Path)**: یه مسیر مخفی و تصادفی برای کانفیگ‌ها.
   - **UUID / Trojan Password**: به‌صورت خودکار ساخته می‌شن.
4. دکمه نصب رو بزنید؛ بعد از چند ثانیه **آدرس پنل** بهتون داده می‌شه. ✅
5. ویزارد بعد از اولین نصب یه **Private Link** هم می‌ده که نصب‌های بعدی رو روی همون اکانت **تک‌کلیکی** می‌کنه — جایی امن نگهش دارید.

---

## ۳. روش ۲: نصب با Wizard در ترمینال (CLI)

نسخه CLI برای ویندوز، اندروید، لینوکس و مک در دسترسه و از **چند اکانت مختلف** پشتیبانی می‌کنه (لاگین‌ها روی دستگاه خودتون ذخیره می‌شن).

### ویندوز (PowerShell)

<div dir="ltr">

```powershell
irm https://raw.githubusercontent.com/bia-pain-bache/BPB-Wizard/main/install.ps1 | iex
```

</div>

### اندروید (Termux) — لینوکس — مک

<div dir="ltr">

```bash
bash <(curl -fsSL https://raw.githubusercontent.com/bia-pain-bache/BPB-Wizard/main/install.sh)
```

</div>

> ⚠️ **نکات مهم Termux**
> - ترمیوکس رو حتماً [از ریلیزهای رسمی گیت‌هاب](https://github.com/termux/termux-app/releases/latest) نصب کنید، **نه** گوگل‌پلی (نسخه گوگل‌پلی قدیمیه و مشکل ایجاد می‌کنه).
> - ترجیحاً قبل از اجرای اسکریپت، فیلترشکن رو **قطع** کنید.

بعد از اجرا، اسکریپت شما رو قدم‌به‌قدم راهنمایی می‌کنه: ورود با API Token، انتخاب Workers یا Pages، و تنظیم پسورد پنل و مسیر امن — دقیقاً مثل نسخه وب.

---

## ۴. روش ۳: بیلد نسخه سفارشی (مخصوص توسعه‌دهنده‌ها)

اگه خواستید کدهای این فورک (DogHub) رو شخصی‌سازی کنید یا تغییرات بدید، می‌تونید خودتون بیلد بگیرید.

**پیش‌نیاز:** Node.js نسخه ۲۰ به بالا

<div dir="ltr">

```bash
git clone https://github.com/jjgadradan-dot/BPB-Worker-Panel.git
cd BPB-Worker-Panel
npm install
npm run build
```

</div>

خروجی فایل `dist/worker.js` هست (یه فایل تک‌فایلی شامل کل پنل).

برای بررسی صحت کد قبل از بیلد:

<div dir="ltr">

```bash
npm run check
```

</div>

> ⚠️ **نکته مهم:** پنل v5 برای اجرا به تنظیمات جاسازی‌شده (`EMBEDED_SETTINGS`) نیاز داره که یا از طریق **BPB Wizard** موقع نصب ساخته می‌شن یا به‌صورت دستی (روش ۴) به ابتدای اسکریپت اضافه می‌شن.

---

## ۵. روش ۴: نصب دستی روی Cloudflare (بدون ویزارد)

اگه نمی‌خواید از ویزارد استفاده کنید، می‌تونید پنل رو مستقیم و دستی روی اکانت Cloudflare خودتون نصب کنید. این روش کمی فنی‌تره ولی کنترل کامل روی همه چیز بهتون می‌ده.

### گام ۱: آماده کردن فایل `worker.js`

دو راه دارید:

- **بیلد از سورس این فورک (DogHub):**

  <div dir="ltr">

  ```bash
  git clone https://github.com/jjgadradan-dot/BPB-Worker-Panel.git
  cd BPB-Worker-Panel
  npm install
  npm run build
  ```

  </div>

  خروجی: `dist/worker.js`

- **دانلود بیلد رسمی آخرین نسخه:**

  <div dir="ltr">

  ```url
  https://github.com/bia-pain-bache/BPB-Worker-Panel/releases/latest/download/worker.js
  ```

  </div>

### گام ۲: ساخت KV Namespace

پنل برای ذخیره پسورد، تنظیمات و Warp به KV نیاز داره:

1. وارد داشبورد Cloudflare بشید → **Storage & Databases → KV**
2. **Create namespace** رو بزنید و یه اسم بدید (مثلاً `doghub-kv`).

### گام ۳: ساخت API Token (اختیاری ولی پیشنهادی)

توکن برای آپدیت داخل پنل، دامنه اختصاصی و Warp استفاده می‌شه. بدون توکن، خود پنل و کانفیگ‌ها کار می‌کنن ولی این قابلیت‌ها فعال نمی‌شن.

1. **My Profile → API Tokens → Create Token**
2. قالب **Edit Cloudflare Workers** رو انتخاب کنید (اگه بعداً دامنه اختصاصی خواستید، دسترسی **DNS → Edit** رو هم بهش اضافه کنید).
3. توکن رو بسازید و **همون لحظه کپی** کنید.

### گام ۴: ساخت Worker و افزودن تنظیمات

1. از داشبورد برید به **Compute (Workers & Pages) → Create → Worker**
2. یه اسم بدید (مثلاً `doghub`) و **Deploy** کنید، بعد **Edit code** رو بزنید.
3. در **خط اول** ادیتور، این بلوک رو بچسبونید و مقادیر داخلش رو پر کنید:

   <div dir="ltr">

   ```js
   Object.assign(globalThis, {
       EMBEDED_SETTINGS: {
           accID: "ACCOUNT_ID",
           accEmail: "you@example.com",
           apiToken: "YOUR_API_TOKEN",
           vlUUID: "A_RANDOM_UUID",
           trPass: "A_RANDOM_STRONG_PASSWORD",
           securePath: "MySecretPath123",
           proxyIpMode: "proxyip",
           proxyIPs: [],
           prefixes: [],
           fallback: "",
           dohUrl: "https://cloudflare-dns.com/dns-query",
           mainDomain: "doghub.yourname.workers.dev"
       }
   });
   ```

   </div>

4. کل محتوای فایل `worker.js` (گام ۱) رو **زیر همین بلوک** بچسبونید و **Deploy** بزنید.

**معرفی فیلدها:**

| فیلد | مقدار |
|---|---|
| `accID` | شناسه اکانت — از صفحه اصلی داشبورد، بخش **Account ID** (سمت راست صفحه) کپی کنید |
| `accEmail` | همون ایمیلی که باهاش وارد Cloudflare می‌شید |
| `apiToken` | توکنی که تو گام ۳ ساختید |
| `vlUUID` | یه UUID تصادفی — از [uuidgenerator.net](https://www.uuidgenerator.net/) یا هر ابزار مشابه |
| `trPass` | یه رشته تصادفی قوی (پسورد Trojan) |
| `securePath` | مسیر مخفی پنل — حروف انگلیسی، عدد، `-` و `_` (مثلاً ۱۶ کاراکتر تصادفی) |
| `proxyIpMode` | `proxyip` یا `prefix` (برای NAT64) |
| `proxyIPs` | لیست Proxy IPها — خالی `[]` یعنی پیش‌فرض عمومی |
| `prefixes` | لیست پیشوندهای NAT64 — خالی `[]` یعنی پیش‌فرض |
| `fallback` | آدرس fallback (می‌تونه خالی باشه) |
| `dohUrl` | سرور DoH — پیش‌فرض Cloudflare خوبه |
| `mainDomain` | آدرس ورکر شما **بدون `https://`** — دقیقاً همونی که تو گام ۴ ساختید (مثلاً `doghub.yourname.workers.dev`) — توی لینک کانفیگ‌ها استفاده می‌شه |

### گام ۵: اتصال KV به ورکر

1. وارد تنظیمات همون ورکر بشید → **Settings → Bindings**
2. **Add binding → KV Namespace** رو بزنید.
3. **Variable name باید دقیقاً `kv` باشه** (حروف کوچک) و KV ساخته‌شده تو گام ۲ رو انتخاب کنید.
4. ذخیره و Deploy مجدد.

> ⚠️ **مهم:** متغیر محیطی `UUID` یا `TR_PASS` تعریف **نکنید**! پنل v5 اگه این متغیرها رو ببینه فکر می‌کنه نصب قدیمیه و خطا می‌ده.

### گام ۶: باز کردن پنل

آدرس پنل شما این شکلیه:

<div dir="ltr">

```
https://doghub.yourname.workers.dev/MySecretPath123/panel
```

</div>

چون هنوز پسوردی تنظیم نشده، پنل پنجره **Set Password** نشون می‌ده:

- **Username:** ایمیل اکانت (`accEmail`)
- **Password:** یه پسورد قوی — حداقل ۸ کاراکتر، شامل حرف بزرگ و عدد

از دفعه بعد، ورود با همون پسورد انجام می‌شه. همین!

---

## ۶. اولین ورود به پنل

1. آدرسی که ویزارد بهتون داده رو باز کنید، چیزی شبیه این:
   <div dir="ltr">

   ```
   https://my-panel.my-account.workers.dev/MySecretPath123
   ```

   </div>

2. در صفحه لاگین وارد کنید:
   - **Username:** ایمیل اکانت Cloudflare شما
   - **Password:** پسوردی که موقع نصب تنظیم کردید
3. بعد از ورود، پنل DogHub با تب‌های تنظیمات و کانفیگ‌ها پیش‌روتونه.

> 🔐 آدرس پنل شما شامل مسیر امن (Secure Path) هست — همین مسیر باعث می‌شه پنل برای غریبه‌ها قابل حدس نباشه. آدرس رو برای خودتون نگه دارید.

---

## ۷. دریافت کانفیگ‌ها

1. از منوی پنل به تب **Configs** برید.
2. روی **Best Pings** کلیک کنید تا بهترین IPها بر اساس پینگ شما پیدا بشن.
3. **Generate Configs** رو بزنید تا لینک اشتراک (Subscription) ساخته بشه.
4. لینک اشتراک رو در برنامه کلاینتتون وارد کنید (v2rayNG، Streisand، sing-box، Hiddify و…).
5. حالا می‌تونید IP تمیز، Proxy IP، پورت‌ها، Warp و بقیه تنظیمات رو از تب‌های پنل تغییر بدید و دوباره کانفیگ بگیرید.

فهرست کامل برنامه‌های پشتیبانی‌شده و حداقل نسخه‌شون رو [از اینجا ببینید](https://bia-pain-bache.github.io/BPB-Worker-Panel/fa/usage/supported-clients/).

---

## ۸. آپدیت و حذف پنل

- **آپدیت:** وقتی نسخه جدید منتشر بشه، خود پنل بهتون اطلاع می‌ده و با دکمه **Update** در چند ثانیه آپدیت می‌شه (تنظیمات و کانفیگ‌هاتون حفظ می‌شه). ⚠️ اگه دستی نصب کردید یا از فورک DogHub استفاده می‌کنید، دکمه Update نسخه رسمی ریپوی اصلی رو نصب می‌کنه — برای نسخه خودتون دوباره بیلد بگیرید و کد رو در ادیتور ورکر جایگزین کنید.
- **حذف:** از داخل پنل دکمه **Delete** رو بزنید، یا از داشبورد Cloudflare کاربر Worker/Pages مربوطه رو حذف کنید.
- **عیب‌یابی:** اگه پنل باز نشد، اول مطمئن شید مسیر امن رو درست وارد کرده‌اید (بدون `/` اضافه اول و آخر)، بعد [سوالات متداول](https://bia-pain-bache.github.io/BPB-Worker-Panel/en/faq/) رو چک کنید.

---

## لینک‌های مفید

- [راهنمای کامل تنظیمات پنل](https://bia-pain-bache.github.io/BPB-Worker-Panel/fa/configuration/)
- [نحوه استفاده از کانفیگ‌ها](https://bia-pain-bache.github.io/BPB-Worker-Panel/fa/usage/)
- [ریپوی BPB Wizard](https://github.com/bia-pain-bache/BPB-Wizard)
- [سوالات متداول](https://bia-pain-bache.github.io/BPB-Worker-Panel/en/faq/)

---

<details>
<summary>🌐 Installation guide in English</summary>

See [INSTALL.md](INSTALL.md) for the English version of this guide.

</details>
