# FishVisionAR — Android distribution

Public distribution point for the **FishVisionAR Android SDK**
(`app.fishbuddy:fish-vision-ar`). This repository holds no source code — it
serves the released binaries:

- a static **Maven repository** on the `gh-pages` branch, published at
  <https://fiskher.github.io/fish-vision-ar-android-releases/>
- the on-device **TensorFlow Lite models** as GitHub Release assets
  (tag `models-v1`)

Development happens in a private repository. Issues opened here will not be
seen — contact `licensing@fishbuddy.app`.

## Integration

```kotlin
// settings.gradle.kts
dependencyResolutionManagement {
    repositories {
        google()
        mavenCentral()
        maven { url = uri("https://fiskher.github.io/fish-vision-ar-android-releases") }
    }
}

// app/build.gradle.kts
dependencies {
    implementation("app.fishbuddy:fish-vision-ar:0.1.0")
}
```

No Gradle credentials are required — this repository is public. **A valid
licence key is still required at runtime**: every scan validates the key against
the FishVisionAR licence backend, and the SDK refuses to scan without one.
Request a key from `licensing@fishbuddy.app`; keys are issued per
`applicationId` and an exact match is required.

Full integration walkthrough and API reference are supplied with your licence.

## Models

The SDK downloads two `.tflite` files on first use from the `models-v1` release
assets. They can also be bundled in your app's
`assets/fishvisionar/models/v1/`, or served from your own mirror via
`ARScannerConfiguration.modelBaseURL`.

Model updates ship under a **new** release tag with a new default URL. Bytes
already published under an asset name are never rewritten, so a copy cached on a
device stays valid for the SDK version that downloaded it.

## Licence

The binaries distributed here are commercial intellectual property of
Fishbuddy AS, licensed for use **only inside an application holding a valid
FishVisionAR licence**. Public availability of these files is a distribution
convenience and does not grant a licence to use them. See [`LICENSE`](LICENSE).

The `.tflite` model files and their label data are separately protected as
commercially valuable trade secrets. Redistributing them, or extracting them
from a licensed application for use elsewhere, is not permitted.
