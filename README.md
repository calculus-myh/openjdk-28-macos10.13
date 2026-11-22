# OpenJDK 28 (macOS 10.13 High Sierra Unofficial Build)

Unofficial OpenJDK 28 build for macOS 10.13 (High Sierra) with Clang 20.

This is an unofficial build of OpenJDK 28, specifically patched and compiled to run on macOS 10.13.6 (High Sierra) on Intel x86_64 architecture. 

Since official JDK 28 support for x64 macOS (JEP 541) has been deprecated and requires macOS 11+, this build was created to extend the life of legacy Intel Macs.

## How it was built
- Toolchain: Custom-built LLVM/Clang 20.1.8 (via MacPorts) + Xcode 9.4.1 (macOS 10.13 SDK).
- Boot JDK: JDK 27 (compiled locally).
- Patches applied:
  - Removed hardcoded `-mmacosx-version-min=11.00.00` linker flags.
  - Disabled Metal shader compilation (macOS 10.13 does not support Metal).
  - Replaced macOS 10.14+ APIs (`selectedContentBackgroundColor`, `NSWorkspaceOpenConfiguration`, etc.) with legacy equivalents.
  - Fixed `_objc_alloc_init` symbol missing errors by replacing `NSAutoreleasePool` with `@autoreleasepool` syntax sugar.

## Test Results
- `test/hotspot/jtreg:tier1`: 3551 PASS, 0 ERROR
- `test/jdk:tier1`: 2590 PASS, 0 ERROR
- `test/langtools:tier1`: 2966 PASS, 4 ERROR (Due to system localization and environment missing `gtest`).

## Installation
1. Download `jdk28-macos10.13-bin.tar.gz` from the Releases page.
2. Extract to 
- System-wide: /Library/Java/JavaVirtualMachines
- User-local: ~/Library/Java/JavaVirtualMachines.
3. Verify with `./jdk-28.jdk/Contents/Home/bin/java -version`.

## License
This build is based on OpenJDK and is licensed under GPLv2 with Classpath Exception. The modified source code is available in this repository or in the release assets.
