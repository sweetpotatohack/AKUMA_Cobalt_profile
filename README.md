# AKUMA GMAIL PROFILE - 悪魔の偽装通信プロファイル

"In the encrypted arteries of cyberspace, AKUMA masquerades as the mundane."

---

## 🥷 概要 (Overview)

**AKUMA Gmail Profile** is an ultra-stealthy Malleable C2 profile for Cobalt Strike, designed to cloak your Beacon traffic in the skin of Google's Gmail services. Engineered for Red Team operations where OPSEC is paramount, this profile deceives defenders by mimicking legitimate browser-based communication with Gmail.

Forged in the glowing code-forges beneath Tokyo's cyber underworld, this profile doesn't just hide — it misleads.

---

## 🔥 特徴 (Features)

### ☁️ **Gmail Traffic Emulation**

* Realistic HTTP headers, URIs, User-Agent and JavaScript-like response content
* TLS certificate forged to imitate Google’s own (CN=gmail.com, O=Google GMail, etc.)

### 🛡️ **Defender/EDR Reconnaissance**

* Embedded PowerShell & Tasklist execs:

  * `Get-MpComputerStatus`
  * `tasklist | findstr MsMpEng`
* Results sent back through normal C2 output, visible in console or logs

### 🧬 **Dynamic Pipe Masking**

* Named pipe: `chrome-sync-%rand%`
* Mimics background browser sync behavior, blends in on host system

### 💉 **Post-Ex Stealth Ready**

* `spawnto_x86`: `%windir%\\syswow64\\PresentationHost.exe`
* `spawnto_x64`: `%windir%\\sysnative\\PresentationHost.exe`
* Avoids EDR flags on common LOLBins like `rundll32.exe`

### 📡 **Noise-Evading URIs**

* GET: `/mail/u/0/view-tl`
* POST: `/mail/u/0/upload?ui=...`
* No suspicious query strings or anomalies

### ⚙️ **Beacon Stability**

* `sleeptime`: 1000 ms (1s)
* `jitter`: 25%
* Perfect for sandbox evasion and slow-beacon campaigns

### 🧙‍♂️ **Compatible with Redirectors**

* TLS certificate support allows for seamless use with Apache/nginx C2 redirectors

---

## 💀 OPSEC Killer Moves

| Feature                   | Why it matters for Red Team  | What it breaks for Blue Team    |
| ------------------------- | ---------------------------- | ------------------------------- |
| Gmail-style C2 traffic    | Looks 100% legit             | Bypasses proxy alerts, DPI      |
| Defender detection BOF    | Know protection level early  | EDRs can't detect being watched |
| Non-standard spawn host   | No rundll32 = no red flag    | Bypasses common heuristics      |
| Named pipe camouflage     | Blends with browser behavior | No unusual pipe names           |
| No query in GET URI       | Matches normal web traffic   | Stops signature-based rules     |
| Host-stage warning active | Forces redirector hygiene    | Can't download payload openly   |

---

## ☠️ 使い方 (How to Deploy)

1. Clone and import the profile into Cobalt Strike:

```bash
./c2lint gmail-stealth-defender-verified.profile
```

2. Set it in your listener:

```cobalt
use http
set profile gmail-stealth-defender-verified.profile
```

3. Launch Beacons using stageless or redirector-linked stages

---

## 🧪 テスト済み (Tested On)

* Cobalt Strike 4.8+
* Windows 10/11 (x86 & x64)
* Works behind most corporate proxy setups

---

## ⚠️ 免責事項 (Disclaimer)

このプロファイルは合法的なレッドチーム活動また профессионального тестирования на проникновение 専用です。

> "Demon masks as mail — and the SOC doesn’t blink."

---

## 🔗 Github

**Repo:** [https://github.com/sweetpotatohack/AKUMA\_gmail\_profile](https://github.com/sweetpotatohack/AKUMA_Cobalt_profile)
**License:** BSD 3-Clause (血の誓約 / Blood Oath)

# AKUMA GMAIL PROFILE — Профиль стелс-трафика Gmail

"В зашифрованных артериях сети AKUMA принимает облик почтовика..."

---

## 🥷 ОБЗОР

**AKUMA Gmail Profile** — это профиль Malleable C2 для Cobalt Strike, который полностью мимикрирует сетевой трафик Gmail. Профиль создан для Red Team-операций, где OPSEC — всё.

После загруженного в миру почтовых пакетов, AKUMA заговаривает SOC...

---

## 🔥 ОСОБЕННОСТИ

### 📬 Почтовая маскировка

* Реалистичные HTTP-заголовки, URI, User-Agent
* Сертификат TLS, подстроенный под gmail.com

### 🦠 Обнаружение Defender/EDR

* Внутри Beacon встроены вызовы:

  * PowerShell: `Get-MpComputerStatus`
  * CMD: `tasklist | findstr MsMpEng`
* Результат отправляется в C2 канал

### 💠 Тайный SMB канал

* Pipe: `chrome-sync-%rand%`
* Маскируется под Chrome/браузерную синхронизацию

### 🧬 Стелс-спаун в пост-эксплуатации

* x86: `%windir%\syswow64\PresentationHost.exe`
* x64: `%windir%\sysnative\PresentationHost.exe`

### 📡 Реалистичные URI

* GET: `/mail/u/0/view-tl`
* POST: `/mail/u/0/upload?...`

### 🧪 Стабильность Beacon

* Sleeptime: 1000 мс
* Jitter: 25%

### 🔀 Совместимость с Redirector

* Через nginx / Caddy / Apache C2 прокси

---

## 💀 ЧТО ЭТО РАЗНОСИТ

| Фича                     | Для Red Team                       | Для Blue Team        |
| ------------------------ | ---------------------------------- | -------------------- |
| Gmail-трафик             | Выглядит как реальный браузер      | Проходит DPI, прокси |
| Встроенный детектор EDR  | Узнаешь о защите до пост-эксплоита | Сорвана невидимость  |
| Спаун в PresentationHost | Обход регулярных сигнатур EDR      | Не отслеживается     |
| Pipe под Chrome          | Слияние с фоновым трафиком         | Отсутствие алертов   |
| URI без `?`              | Не подпадает под regex-сигнатуры   | Не запинит защиту    |

---

## 🛠 КАК ИСПОЛЬЗОВАТЬ

1. Проверка:

```bash
./c2lint gmail-stealth-defender-verified.profile
```

2. Импорт в листенер:

```cobalt
use http
set profile gmail-stealth-defender-verified.profile
```

3. Старт Beacon с payload/стейджера

---

## 💻 Тестировано на:

* Cobalt Strike 4.8+
* Windows 10/11 x86/x64
* Работает через прокси/файрвол без детекта

---

## ⚠️ ОТВЕТСТВЕННОСТЬ

Этот профиль должен быть использован только в рамках законных проверок и тестов безопасности.

> Почтовый трафик с душой демона. SOC не вспышнет.

---

## 🔗 GitHub

**Repo:** [https://github.com/sweetpotatohack/AKUMA\_gmail\_profile](https://github.com/sweetpotatohack/AKUMA_Cobalt_profile)
**Лицензия:** BSD 3-Clause (Кровавая клятва)
