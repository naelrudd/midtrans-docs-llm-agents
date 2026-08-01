---
updatedAt: 2026-06-24T04:26:53.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Getting Started

# GoPayEnterprise SDK — Client Integration Guide

This guide provides step-by-step instructions for integrating the GoPayEnterprise SDK into your iOS application.

## Distribution Package

The SDK is delivered as one compressed file:

```text
GoPayEnterpriseSDK_{VERSION}.tar.gz
```

Extract once and you get:

```text
GoPayEnterpriseSDK/
└── GoPayEnterprise/
    ├── GoPayEnterprise.podspec
    ├── Frameworks/
    │   ├── GoPayEnterprise.xcframework
    │   └── Ojo.xcframework
    ├── DigitalIdentityModule/
    │   └── DigitalIdentity.xcframework
    └── DigitalIdentityResources.bundle
```

DigitalIdentity is **embedded inside** `GoPayEnterprise.xcframework`. The bundled `DigitalIdentityModule/DigitalIdentity.xcframework` puts the DI module on your compiler's search path (with autolink disabled) — you do not link it separately. Install and use the single `GoPayEnterprise` pod only.

## Requirements

| Requirement | Minimum |
| ----------- | ------- |
| iOS         | 14.0    |
| Xcode       | 16.0    |
| Swift       | 5.0     |
| CocoaPods   | Latest  |

## Installation

### 1. Place SDK files

Extract `GoPayEnterpriseSDK_{VERSION}.tar.gz` into your project directory (alongside your `Podfile`).

### 2. Configure Podfile

```ruby
platform :ios, '14.0'

source 'https://cdn.cocoapods.org/'

target 'YourApp' do
  use_frameworks!

  pod 'GoPayEnterprise', :path => './GoPayEnterpriseSDK/GoPayEnterprise'
end

post_install do |installer|
  installer.pods_project.targets.each do |target|
    if ["SwiftProtobuf", "SSZipArchive", "ReachabilitySwift", "GRDB.swift", "Starscream"].include?(target.name)
      target.build_configurations.each do |config|
        config.build_settings['BUILD_LIBRARY_FOR_DISTRIBUTION'] = 'YES'
      end
    end
  end
end
```

The `post_install` hook is required. It sets `BUILD_LIBRARY_FOR_DISTRIBUTION` on the specific transitive dependencies that need it.

### 3. Install

```bash
pod install
```

### 4. Open workspace

```bash
open YourApp.xcworkspace
```

## CocoaPods Dependencies

The podspec declares all required dependencies. CocoaPods resolves them automatically.

| Dependency        | Version    |
| ----------------- | ---------- |
| SwiftProtobuf     | \~> 1.30.0 |
| SSZipArchive      | \~> 2.4.3  |
| GRDB.swift        | \~> 6.7.0  |
| Starscream        | 4.0.5      |
| ReachabilitySwift | >= 5.0.0   |

## Required Permissions

Add these entries to your `Info.plist`:

```xml
<key>NSCameraUsageDescription</key>
<string>Camera access is required for identity verification</string>
```

KYC flows (KTP Scan, Selfie Liveness, Selfie Verification, KYC Verification) require camera access.

## Update LSApplicationQueriesSchemes in Info.plist

For security purposes, add the following jailbreak app-related schemes to the `LSApplicationQueriesSchemes` key in your `Info.plist`:

```xml
<key>LSApplicationQueriesSchemes</key>
<array>
  <string>zbra</string>
  <string>cydia</string>
  <string>undecimus</string>
  <string>sileo</string>
  <string>filza</string>
</array>
```

These schemes allow the SDK to detect jailbroken devices for enhanced security checks.