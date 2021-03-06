[![swift-version](https://img.shields.io/badge/swift-5.0-brightgreen.svg)](https://github.com/apple/swift)
[![swift-package-manager](https://img.shields.io/badge/package%20manager-compatible-brightgreen.svg)](https://github.com/apple/swift-package-manager)
[![build-status](https://travis-ci.com/backslash-f/aescryptable.svg?branch=master)](https://travis-ci.com/backslash-f/aescryptable)
[![license](https://img.shields.io/badge/license-mit-brightgreen.svg)](https://en.wikipedia.org/wiki/MIT_License)

# AESCryptable
Provides [`Advanced Encryption Standard (AES)`](https://en.wikipedia.org/wiki/Advanced_Encryption_Standard) capabilities.

- [x] Relies on native [`CCCrypt`](http://bit.ly/cccryptManPages) (via `import CommonCrypto`).
- [x] Uses [`Cipher Block Chaining (CBC)`](https://en.wikipedia.org/wiki/Block_cipher_mode_of_operation#Cipher_Block_Chaining_(CBC)) mode with random [`Initialization Vector (IV)`](https://en.wikipedia.org/wiki/Block_cipher_mode_of_operation#Initialization_vector_(IV)).
- [x] Works (only) with **256-bit** [`key size`](https://en.wikipedia.org/wiki/Key_size). This is by design.
- [x] Uses `kCCOptionPKCS7Padding` as `CCOptions` by default.

## Integration
### Xcode 11+
![AESCryptable Xcode 11 SPM](https://i.imgur.com/JKciz5T.gif)

(More on the topic from WWDC 2019: [Adopting Swift Packages in Xcode](https://developer.apple.com/videos/play/wwdc2019/408/) and [Creating Swift Packages](https://developer.apple.com/videos/play/wwdc2019/410/).)

### Via Package.swift
In your `Package.swift`, add `AESCryptable` as a dependency:
```swift
dependencies: [
  // 🔐 AES encryption/decryption with random iv. Swift 5 and up.
  .package(url: "https://github.com/backslash-f/aescryptable", from: "1.0.0")
],
```

Associate the dependency with your target:
```swift
targets: [
  .target(name: "App", dependencies: ["AESCryptable"])
]
```
Run: `swift build`

## Usage
```swift
import AESCryptable

do {
  // encrypt
  let aes = try AES(keyString: "01234567890123456789012345678901")
  let encryptedData = try aes.encrypt("The black knight always triumphs!")

  // decrypt
  let decryptedString = try aes.decrypt(encryptedData)
  print(decryptedString) // The black knight always triumphs!

} catch {
  print(error)
}
```

(Refer to [the test class](https://github.com/backslash-f/aescryptable/blob/master/Tests/AESCryptableTests/AESCryptableTests.swift) for a high-level overview.)

## Demo
Clone the repo and use `AESCryptable.playground` to see the code in action:

![AESCryptable Demo](https://i.imgur.com/6cI5Knu.gif)
