# بستهٔ تحویل پروژهٔ CLXY

این بسته شامل snapshot کامل سورس فعلی، دارایی‌ها و فایل‌های لازم برای بیلد اندروید، دو APK فعلی و کلید امضایی است که با هر دو APK تطبیق داده شد.

## محتویات

- `Project-Source/`: سورس کامل پروژه و دارایی‌هایش؛ فایل `app/android/app/libs/core.aar` هم نگه داشته شده تا بیلد اندروید بدون ساخت دوبارهٔ هستهٔ Go انجام شود.
- `APKs/CLXY-1.0.3-arm64-v8a-release.apk`: خروجی Release فعلی؛ SHA-256: `d97f2ba22f0e3a4721d876de7eb3721d939346d480b27ca6d9dd324812acd1ab`.
- `APKs/CLXY-1.0.3-arm64-v8a-debug-final.apk`: آخرین خروجی Debug از بازطراحی صفحهٔ شروع؛ SHA-256: `e85d4d7ba8abddfbe80f0b68644f474fed12de7bfc28953b6d7f2f15e794abed`.
- `Signing/CLXY-Android-debug.keystore`: کلید امضای دقیقاً مطابق با گواهی امضای هر دو APK.
- `SHA256SUMS.txt`: هش تمام فایل‌های payload برای بررسی سلامت.

## شناسه‌ها و نسخه

- نام قابل‌نمایش: `CLXY`
- شناسهٔ نصب اندروید / application ID: `com.clxy.android`
- Android namespace داخلی: `com.arman.firefoxvpn`
- نسخهٔ Flutter در سورس: `1.0.3+121`؛ نام نسخه `1.0.3` است و کد build نسخهٔ ARM64 فعلی `2121` است.
- هر دو APK با SHA-256 گواهی `e028b2d6609bdb919edb48d1050cd993e46aa4acc0e1f09657150b9debbbd405` امضا شده‌اند.

## پیش‌نیازهای بیلد

برای بیلد اندروید از Flutter `3.47.8` / Dart `3.13.7`، Java `21`، Android SDK platform/build-tools `36`، NDK `30.0.16248370` و Gradle Wrapper `9.3.1` استفاده شده است. فایل `app/android/local.properties` عمداً داخل بسته نیست، چون مسیرهای SDK/Flutter به هر دستگاه وابسته‌اند. آن را بسازید و مسیرهای مطلق همان دستگاه را قرار دهید:

```properties
sdk.dir=/مسیر/مطلق/Android/Sdk
flutter.sdk=/مسیر/مطلق/flutter
```

## بیلد و امضای Release

از ریشهٔ همین بسته، کلید را در مسیر محلی پروژه کپی کنید و فایل پیکربندی امضا را بسازید. این دو فایل محلی را در Git یا مخزن عمومی قرار ندهید:

```bash
cp Signing/CLXY-Android-debug.keystore Project-Source/app/android/release.jks
cat > Project-Source/app/android/key.properties <<'EOF'
storeFile=../release.jks
storePassword=android
keyAlias=androiddebugkey
keyPassword=android
EOF
cd Project-Source/app
flutter pub get
flutter analyze
flutter test
flutter build apk --release --split-per-abi --target-platform android-arm64 \
  --build-name=1.0.3 --build-number=121 \
  --dart-define=APP_VERSION=1.0.3
```

فایل خروجی معمولاً در `Project-Source/app/build/app/outputs/flutter-apk/app-arm64-v8a-release.apk` ساخته می‌شود. پیش از نصب یا انتشار، package، نسخه، ABI و گواهی را بررسی کنید. چون buildهای split برای ARM64 کد `2121` دارند، آن را با نسخهٔ نصب‌شده تطبیق دهید.

## کلید امضا، محرمانگی و بازتولید هسته

- Alias: `androiddebugkey`
- رمز keystore: `android`
- رمز کلید خصوصی: `android`
- اثرانگشت گواهی SHA-256: `e028b2d6609bdb919edb48d1050cd993e46aa4acc0e1f09657150b9debbbd405`

این کلید از نوع debug است و رمز پیش‌فرض آن عمومی و شناخته‌شده است؛ خود فایل کلید را محرمانه نگه دارید و در GitHub، چت عمومی یا مخزن عمومی نگذارید. این بسته بنا به درخواست مالک شامل کلید است. اطلاعات ورود حساب‌های بیرونی، API token یا دادهٔ شخصی نامرتبط داخل بسته قرار نگرفته است.

سورس Go هم داخل `Project-Source/core/` است. برای بیلد معمول اپ، `core.aar` حاضر است و Go لازم نیست. فقط اگر هستهٔ Go را تغییر دادید و باید AAR را دوباره تولید کنید، نسخهٔ Go موردنیاز ماژول و دستورهای gomobile را در `Project-Source/core/go.mod` و `Project-Source/core/doc/DEVELOPMENT.md` بررسی کنید.

## نکتهٔ مربوط به تاریخچه

این workspace پوشهٔ `.git` یا تاریخچهٔ قابل‌اعتماد Git ندارد؛ تحویل یک snapshot از سورس موجود است، نه مخزن دارای commit history. برای کوچک ماندن بسته، فقط کش‌ها و خروجی‌های بازتولیدشدنی Flutter/Gradle، فایل محلی `local.properties` و پوشه‌های `ephemeral` حذف شده‌اند؛ سورس، تست‌ها، اسناد، دارایی‌ها و فایل AAR لازم نگه داشته شده‌اند.
