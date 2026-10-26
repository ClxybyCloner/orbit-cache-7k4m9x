# CLXY handoff

Complete source snapshot, build assets, two Android APKs, and their matching Android signing keystore. The owner explicitly approved publishing the source and signing key publicly. This repository is a handoff snapshot, not the updater repository, and contains no Git history from the original project.

**Signing-key notice:** the included key is public. Anyone with this package can sign builds with it, so its certificate must not be treated as proof that a build came from the owner. Older confidentiality wording in the original build guide predates this explicit public-publication approval.

## Download

[Open the handoff release](https://github.com/ClxybyCloner/orbit-cache-7k4m9x/releases/tag/handoff-20261027). No GitHub sign-in is needed. The large binary parts are release assets; the repository's “Download ZIP” contains the guides, not these parts.

Download these five parts. Keep their names unchanged and put all five in one folder:

- [CLXY-Handoff-20261027.zip.part-00](https://github.com/ClxybyCloner/orbit-cache-7k4m9x/releases/download/handoff-20261027/CLXY-Handoff-20261027.zip.part-00)
- [CLXY-Handoff-20261027.zip.part-01](https://github.com/ClxybyCloner/orbit-cache-7k4m9x/releases/download/handoff-20261027/CLXY-Handoff-20261027.zip.part-01)
- [CLXY-Handoff-20261027.zip.part-02](https://github.com/ClxybyCloner/orbit-cache-7k4m9x/releases/download/handoff-20261027/CLXY-Handoff-20261027.zip.part-02)
- [CLXY-Handoff-20261027.zip.part-03](https://github.com/ClxybyCloner/orbit-cache-7k4m9x/releases/download/handoff-20261027/CLXY-Handoff-20261027.zip.part-03)
- [CLXY-Handoff-20261027.zip.part-04](https://github.com/ClxybyCloner/orbit-cache-7k4m9x/releases/download/handoff-20261027/CLXY-Handoff-20261027.zip.part-04)

Also download [SHA256SUMS-PARTS.txt](SHA256SUMS-PARTS.txt). These are binary pieces of **one ordinary ZIP**, not independent archives. Do not extract a part on its own.

## Reassemble and verify

Run these commands inside the folder containing all five parts.

### Linux / macOS

```bash
# Verify parts: Linux
sha256sum -c SHA256SUMS-PARTS.txt
# On macOS use this instead:
# shasum -a 256 -c SHA256SUMS-PARTS.txt

cat CLXY-Handoff-20261027.zip.part-00 CLXY-Handoff-20261027.zip.part-01 CLXY-Handoff-20261027.zip.part-02 CLXY-Handoff-20261027.zip.part-03 CLXY-Handoff-20261027.zip.part-04 > CLXY-Handoff-20261027.zip
unzip -t CLXY-Handoff-20261027.zip
unzip CLXY-Handoff-20261027.zip
```

### Windows Command Prompt (CMD, not PowerShell)

```bat
copy /b CLXY-Handoff-20261027.zip.part-00+CLXY-Handoff-20261027.zip.part-01+CLXY-Handoff-20261027.zip.part-02+CLXY-Handoff-20261027.zip.part-03+CLXY-Handoff-20261027.zip.part-04 CLXY-Handoff-20261027.zip
certutil -hashfile CLXY-Handoff-20261027.zip SHA256
```

Expected SHA-256 of the reconstructed ZIP:

```text
6aba5c187a29065bbfd3015eb10340bcd4bbdcf23560410509fb1a13724697ed
```

Compare the hash before extracting the resulting ZIP with Windows Explorer or 7-Zip.

The archive contains `Payload/Project-Source/`, `Payload/APKs/`, `Payload/Signing/`, the build guide `Payload/README-FA.md`, and payload checksums. A standalone copy of the original [Persian build guide](README-FA.md) is also provided here. See [REASSEMBLE-FA.txt](REASSEMBLE-FA.txt) for the original reconstruction notes.

## راهنمای فارسی

از پنج لینک دانلود بالای صفحه یا بخش **Assets** ریلیز، فایل‌های `part-00` تا `part-04` را بگیر و کنار هم در یک پوشه بگذار. نامشان را تغییر نده. گزینهٔ «Download ZIP» خود مخزن فقط راهنماها را می‌گیرد، نه قطعه‌های اصلی. هر قطعه را جداگانه Extract نکن؛ این‌ها پنج تکهٔ باینری از یک ZIP معمولی‌اند.

در لینوکس یا مک دستور `cat` بالا، و در ویندوز داخل **Command Prompt / CMD** دستور `copy /b` بالا را اجرا کن. خروجی `CLXY-Handoff-20261027.zip` است. هش SHA-256 آن باید دقیقاً با مقدار بالا یکی باشد؛ بعد ZIP نهایی را Extract کن.

داخل `Payload` سورس کامل، فایل‌های لازم برای بیلد، دو APK و کلید امضای مطابق با آن‌ها قرار دارد. راهنمای بیلد در `Payload/README-FA.md` است. فایل `SHA256SUMS.txt` داخل بسته برای بررسی سلامت فایل‌های استخراج‌شده است.

انتشار عمومی سورس و کلید با تأیید صریح مالک انجام شده؛ هشدار محرمانگی در راهنمای قدیمی مربوط به قبل از این تأیید است. این کلید از این به بعد عمومی است و هر کسی می‌تواند با آن فایل را امضا کند. این مخزن فقط برای تحویل پروژه است و به مخزن آپدیت برنامه دست نمی‌زند.
