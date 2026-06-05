# DayTracker - Kun hisoblagich

## Dastur nima qiladi?
- Birinchi ochganda sana tanlaysiz (1-kun shu sana bo'ladi)
- Har kun o'tganda raqam 1 ga oshadi (1→2→3→...→15→1→2→...)
- **Widget** — uy ekraniga qo'shsa bo'ladi, u yerda ham kun raqami ko'rinadi
- Har kuni avtomatik yangilanadi

## APK qilish (2 yo'l)

### 1-yo'l: Android Studio (eng oson)
1. Android Studio ni oching: https://developer.android.com/studio
2. File → Open → bu papkani tanlang
3. Build → Build APK(s)
4. APK: `app/build/outputs/apk/debug/app-debug.apk`

### 2-yo'l: GitHub Actions (bepul, online)
1. GitHub da yangi repo oching
2. Bu papkadagi fayllarni yuklang
3. `.github/workflows/build.yml` fayl qo'shing (quyida)
4. Actions tab da APK yuklab oling

### GitHub Actions workflow:
```yaml
name: Build APK
on: [push]
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - uses: actions/setup-java@v3
        with:
          java-version: '17'
          distribution: 'temurin'
      - run: chmod +x gradlew
      - run: ./gradlew assembleDebug
      - uses: actions/upload-artifact@v3
        with:
          name: app-debug
          path: app/build/outputs/apk/debug/app-debug.apk
```

## Logika
- Start sana saqlanadi (SharedPreferences)
- Bugungi sana - start sana = necha kun o'tgan
- (o'tgan kun % 15) + 1 = joriy kun
- 15 kundan keyin avtomatik 1 ga qaytadi
