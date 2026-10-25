# Mags

Onofficiële client voor [Magister](https://www.magister.nl). Kotlin Multiplatform + Compose Multiplatform: **één codebase, Android en Windows-desktop**.

Mags is **geen** product van Iddink/Magister. Werkt met elke Magister-school. Alleen de ingelogde leerling ziet de eigen data.

## Schrijven in common, shippen in beide

Toekomstige features en fixes horen in `:core`:

| Source set | Wat erin zit |
|---|---|
| `core/src/commonMain` | expect-API’s, haptics-model, gedeelde Compose-hooks |
| `core/src/androidAndDesktopMain` | Magister-API, DTOs, PKCE, repositories, CacheBlob, ViewModel, alle schermen |
| `core/src/androidMain` | Keystore-tokens, Custom Tabs, WebView, Material You, Pixel-haptics |
| `core/src/jvmMain` | Versleutelde bestanden in het user-profiel, desktop-login |

`:app` is de Android-schil (splash, WorkManager, Glance-widget, Live Update, crash-scherm).
`:desktop` is het Compose Desktop-venster. Beide roepen dezelfde `CitaRoot` / `CitaViewModel` aan.

## Bouwen

Vereist JDK 17+ (21 is ok), Android SDK platform 37.

```bash
export ANDROID_HOME=/pad/naar/android-sdk
./gradlew :core:jvmTest :app:testDebugUnitTest :app:assembleDebug :app:assembleRelease
./gradlew :desktop:createDistributable :desktop:packageDistributionForCurrentOS
```

**Windows-installer (MSI)** — `packageMsi` gebruikt WiX en draait alleen op Windows:

```bat
gradlew.bat :desktop:packageMsi
```

GitHub Actions (`.github/workflows/desktop-msi.yml`) bouwt het MSI op `windows-latest` bij elke push naar `main`, bij tags `v*` (upload naar een GitHub Release) en via *Run workflow*. Dezelfde workflow bouwt de Android-APKs op Ubuntu.

ApplicationId blijft `app.mags` (debug: `app.mags.debug`). Versie **0.2.0**.

## Licentie / verantwoordelijkheid

Alleen voor persoonlijk gebruik van je eigen Magister-account. Endpoints zijn ongedocumenteerd en kunnen breken. Geen garantie.
