---
updatedAt: 2026-04-10T10:29:41.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Getting Started

# &#x20;Requirements

Android 5.0 (API level 21) and above

# Installation

## Manually adding the artifacts

1. Create a libs folder within your module if it does not exist.
2. Paste the given .aar file in the libs folder.
3. Add the following in module’s build.gradle file, replace \<filename> with the .aar file name

```kotlin
dependencies {
  ...
  implementation(files("libs/<filename>.aar"))
}
```

4. Implement the dependencies from the .pom file as well, whichever does not already exist in the
   module’s dependencies. A helper tool to convert the .pom dependencies to gradle/kotlin dsl is to use
   `maven2gradle` or `maven-to-gradle-kotlin-dsl` respectively. It might look something like this:

```groovy
implementation("androidx.databinding:viewbinding:x.y.z")
implementation("androidx.appcompat:appcompat:x.y.z")
//...
implementation("com.squareup.okhttp3:okhttp:x.y.z")
implementation("com.squareup.okhttp3:logging-interceptor:x.y.z")
//...
implementation("com.google.protobuf:protobuf-javalite:x.y.z")
```

5. Once the above implementation is finalised, do **sync project with gradle files**.

## Maven \[Deprecated]

# Dependencies

<br />

| Name                 | Dependency                                       | Version |
| :------------------- | :----------------------------------------------- | :------ |
| Appcompat            | androidx.appcompat:appcompat                     | 1.6.1   |
| Activity             | androidx.activity:activity                       | 1.8.0   |
| Constraint Layout    | androidx.constraintlayout:constraintlayout       | 2.0.1   |
| Core                 | androidx.core:core-ktx                           | 1.10.1  |
| View Binding         | androidx.databinding:viewbinding                 | 7.3.1   |
| Dagger               | com.google.dagger:dagger-android-support         | 2.43.0  |
| Material             | com.google.android.material:material             | 1.4.0   |
| EXIF Interface       | androidx.exifinterface:exifinterface             | 1.3.7   |
| Protobuf Javalite    | com.google.protobuf:protobuf-javalite            | 4.29.3  |
| OkHttp               | com.squareup.okhttp3:okhttp                      | 4.11.0  |
|                      | com.squareup.okhttp3:logging-interceptor         |         |
| Retrofit             | com.squareup.retrofit2:retrofit                  | 2.11.0  |
|                      | com.squareup.retrofit2:converter-gson            |         |
| WorkManager          | androidx.work:work-runtime-ktx                   | 2.8.1   |
|                      | androidx.work:work-testing                       |         |
| Lifecycle            | androidx.lifecycle:lifecycle-livedata-ktx        | 2.6.2   |
|                      | androidx.lifecycle:lifecycle-viewmodel-ktx       |         |
| Coroutines           | org.jetbrains.kotlinx:kotlinx-coroutines-android | 1.7.3   |
|                      | org.jetbrains.kotlinx:kotlinx-coroutines-core    |         |
| Kotlin               | org.jetbrains.kotlin:kotlin-parcelize-runtime    | 1.8.10  |
|                      | org.jetbrains.kotlin:kotlin-stdlib-jdk8          |         |
|                      | org.jetbrains.kotlin:kotlin-stdlib               |         |
| OneKYC \[To confirm] |                                                  |         |

<br />

# Size

Approximately   MB

<br />

# Permissions

| Name                   | Description                                                                                                                              |
| :--------------------- | :--------------------------------------------------------------------------------------------------------------------------------------- |
| CAMERA                 | Required to capture KTP and Selfie images.                                                                                               |
|                        |                                                                                                                                          |
| INTERNET               | Required to connect to backend services and upload documents                                                                             |
| ACCESS\_WIFI\_STATE    | Allows the application to check the state of Wi-Fi connectivity, ensuring smooth operation in network-dependent tasks.                   |
| ACCESS\_NETWORK\_STATE | Enables the application to monitor the device's overall network connectivity, allowing fallback mechanisms if the network state changes. |

# Configurations

<br />

|          | Staging                          | Production                       |
| :------- | :------------------------------- | :------------------------------- |
| clientID | Provided with artifact via Email | Provided with artifact via Email |

<br />