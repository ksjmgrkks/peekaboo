# peekaboo
[![Kotlin](https://img.shields.io/badge/kotlin-1.9.21-blue.svg?logo=kotlin)](http://kotlinlang.org)
[![Compose Multiplatform](https://img.shields.io/badge/Compose%20Multiplatform-v1.5.11-blue)](https://github.com/JetBrains/compose-multiplatform)
[![Maven Central](https://img.shields.io/maven-central/v/io.github.team-preat/peekaboo-image-picker?color=orange)](https://search.maven.org/search?q=g:io.github.team-preat)
[![Apache-2.0](https://img.shields.io/badge/License-Apache%202.0-green.svg)](https://opensource.org/licenses/Apache-2.0)

[![Build](https://github.com/team-preat/peekaboo/actions/workflows/ci_check.yml/badge.svg)](https://github.com/team-preat/peekaboo/actions/workflows/ci_check.yml)
![badge-android](http://img.shields.io/badge/platform-android-6EDB8D.svg?style=flat)
![badge-ios](http://img.shields.io/badge/platform-ios-CDCDCD.svg?style=flat)

📂 Kotlin Multiplatform library for Compose Multiplatform, designed for seamless integration of an image picker feature in iOS and Android applications.

## Getting started

### Compose Multiplatform

`peekaboo` is based on `Compose Multiplatform`, currently targeting only `iOS` and `Android`. <br/>
Please note that it primarily focuses on these platforms, and additional platforms may be considered in the future. <br/>
When using `peekaboo` on Android, ensure that Google's Jetpack Compose version is compatible with `peekaboo`'s Compose Multiplatform version. <br/>

## Installation

The minimum supported Android SDK is 24 (Android 7.0).

In your `commonMain` configuration, add `peekaboo` as a dependency to your project. It's available on Maven Central. 
<br/>
### Without Version Catalog

```kotlin
commonMain {
    dependencies {
        implementation("io.github.team-preat:peekaboo-image-picker:$latest_version")
    }
}
```


### With Version Catalog

First, define the version in `libs.versions.toml`:

```toml
[versions]
peekaboo = "0.2.1"

[libraries]
peekaboo-image-picker = { module = "io.github.team-preat:peekaboo-image-picker", version.ref = "peekaboo" }
```

Then, in your `commonMain` configuration, reference the defined version:

```kotlin
commonMain {
    dependencies {
        implementation(libs.peekaboo.image.picker)
    }
}
```

### Artifacts

| Name                    | Description                                                                 |
|-------------------------|-----------------------------------------------------------------------------|
| `peekaboo-image-picker` | Simplifies the process of selecting single or multiple images in `iOS` and `Android` apps. |
| `peekaboo-camera` | 🚧 Coming soon! A convenient way to capture and select images directly from cameras on iOS and Android. 📸 |

<br/>

## Usage
### Select Single Image

```kotlin
val scope = rememberCoroutineScope()

val singleImagePicker = rememberImagePickerLauncher(
    selectionMode = SelectionMode.Single,
    scope = scope,
    onResult = { byteArrays ->
        byteArrays.firstOrNull()?.let {
            // Process the selected images' ByteArrays.
            println(it)
        }
    }
)

Button(
    onClick = {
        singleImagePicker.launch()
    }
) {
    Text("Pick Single Image")
}
```

| Android                                                         | iOS                                                     |
|-----------------------------------------------------------------|---------------------------------------------------------|
| <img src="https://github.com/TEAM-PREAT/peekaboo/assets/76798309/03346992-cf2a-4424-88e5-fa53afd36eac" width="300" height="700"> | <img src="https://github.com/TEAM-PREAT/peekaboo/assets/76798309/7b562f6f-e5d5-4858-85b8-acf7196d646f" width="300" height="700"> |

Simply select the desired image with an intuitive interface.

<br/>

### Select Multiple Images

If you want to select multiple images, you can use `SelectionMode.Multiple()`. And you can set the maximum number of images to select.
If you didn't set max selection, the default value is maximum number that the system supports.

```kotlin
val scope = rememberCoroutineScope()

val multipleImagePicker = rememberImagePickerLauncher(
    // Optional: Set a maximum selection limit, e.g., SelectionMode.Multiple(maxSelection = 5).
    // Default: No limit, depends on system's maximum capacity.
    selectionMode = SelectionMode.Multiple(maxSelection = 5),
    scope = scope,
    onResult = { byteArrays ->
        byteArrays.forEach {
            // Process the selected images' ByteArrays.
            println(it)
        }
    }
)

Button(
    onClick = {
        multipleImagePicker.launch()
    }
) {
    Text("Pick Multiple Images")
}
```

| Android                                                         | iOS                                                     |
|-----------------------------------------------------------------|---------------------------------------------------------|
| <img src="https://github.com/TEAM-PREAT/peekaboo/assets/76798309/e26ae1b3-4333-41a9-92c3-ebe56c337d79" width="300" height="700"> | <img src="https://github.com/TEAM-PREAT/peekaboo/assets/76798309/a990ce09-d485-4a0f-9416-8af8b040cf2d" width="300" height="700"> |

<br/>

## ByteArray to ImageBitmap Conversion
We've added a new extension function `toImageBitmap()` to convert a `ByteArray` into an `ImageBitmap`. <br/>
This function simplifies the process of converting image data into a displayable format, enhancing the app's capability to handle image processing efficiently.

### Usage
```kotlin
val imageBitmap = byteArray.toImageBitmap()
```

<br/>

## Contributions 🙏

Contributions are always welcome!

If you'd like to contribute, please feel free to create a PR or open an issue. 👍

<br/>

## Stargazers :star:
Support it by joining __[stargazers](https://github.com/TEAM-PREAT/peekaboo/stargazers)__ for this repository. :star: <br>

## License

```
Copyright 2023 onseok

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

   https://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
```
