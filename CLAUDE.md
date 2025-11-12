# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

**xemantic-kotlin-process** is a Kotlin multiplatform library for coroutine-friendly process spawning, designed to be published to Maven Central.

- **Group ID**: `com.xemantic.kotlin.process`
- **Package**: `com.xemantic.kotlin.process`
- **License**: Apache 2.0

## Build Commands

### Standard Build and Test
```shell
./gradlew build
```

### Run All Tests
```shell
./gradlew test
```

### Run Tests for Specific Platform
```shell
./gradlew jvmTest           # JVM tests
./gradlew jsNodeTest        # JS Node.js tests
./gradlew wasmJsNodeTest    # Wasm JS Node.js tests
./gradlew macosArm64Test    # macOS ARM64 tests
```

### Check for Dependency Updates
```shell
./gradlew dependencyUpdates --no-parallel
```

### Generate Documentation
```shell
./gradlew dokkaGenerateHtml
```

### Binary Compatibility Validation
```shell
./gradlew apiCheck
```

## Architecture

### Multiplatform Configuration

This is a **Kotlin Multiplatform library** supporting:
- **JVM** (Java 17 target)
- **JS** (Browser and Node.js)
- **Wasm** (WasmJs and WasmWasi)
- **Native** platforms (macOS, iOS, Linux, Windows, Android Native, watchOS, tvOS)

The project uses:
- **Explicit API mode** (`explicitApi()`) - all public APIs must have explicit visibility modifiers and return types
- **Progressive mode** and **extra warnings** enabled
- **Context parameters** and **context-sensitive resolution** compiler features

### Testing Framework

Tests use the **xemantic-kotlin-test** library with Power Assert:
- Test assertions use `should` and `have` syntax
- Power Assert is configured for `com.xemantic.kotlin.test.assert` and `com.xemantic.kotlin.test.have` functions
- Located in `src/commonTest/kotlin/com/xemantic/kotlin/process/`

### Gradle Conventions

The project uses **xemantic-conventions** plugin which applies common build configurations. Dependencies are managed via `gradle/libs.versions.toml`.

Key configurations:
- Kotlin language version: 2.2
- Java target: 17
- API/Language versions are centrally defined in `libs.versions.toml`

### Publishing

Configured for Maven Central publishing with:
- Automatic snapshot publishing on main branch pushes
- Release publishing via GitHub Actions
- JReleaser integration for announcements (Discord, LinkedIn, Bluesky)
- API binary compatibility validation

### Known Platform Limitations

Some tests are disabled due to XCode component requirements:
- `tvosSimulatorArm64Test`
- `watchosSimulatorArm64Test`

## Source Structure

```
src/
├── commonMain/kotlin/com/xemantic/kotlin/process/  # Platform-agnostic code
└── commonTest/kotlin/com/xemantic/kotlin/process/  # Common tests
```

Platform-specific implementations can be added as:
- `src/jvmMain/`, `src/jvmTest/`
- `src/nativeMain/`, `src/nativeTest/`
- etc.

## Development Notes

### Adding Dependencies

Add dependencies to `gradle/libs.versions.toml` following the existing pattern, then reference them in `build.gradle.kts`.

### Writing New Code

- All public APIs require explicit visibility modifiers (`public`, `internal`, etc.)
- Copyright headers are managed via `.idea/copyright/apache2_0.xml`
- Package structure: `com.xemantic.kotlin.process.*`
