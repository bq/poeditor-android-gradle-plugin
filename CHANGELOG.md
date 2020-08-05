# Changelog
All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]
### Added
- Add support for flavor and build type configuration. The sample configuration is as follows:
<details open><summary>Groovy</summary>

```groovy
poEditor {
    // Default config that applies to all flavor/build type configurations. 
    // Also executed when calling 'importPoEditorStrings'
}

android {
    // If you have the following flavors...
    flavorDimensions 'type'
    productFlavors {
        free { dimension 'type' }
        paid { dimension 'type' }
    }

    poEditorConfig {
        free {
            // Configuration for the free flavor, same syntax as usual
        }
        paid {
            // Configuration for the paid flavor, same syntax as usual
        }
        debug {
            // Configuration for the debug build type, same syntax as usual
        }
        release {
            // Configuration for the release build type, same syntax as usual
        }
    }
}
```

</details>

<details><summary>Kotlin</summary>

```kt
poEditor {
    // Default config that applies to all flavor/build type configurations. 
    // Also executed when calling 'importPoEditorStrings'
}

android {
    // If you have the following flavors...
    flavorDimensions("type")

    productFlavors {
        register("free") { setDimension("type") }
        register("paid") { setDimension("type") }
    }

    poEditorConfig {
        register("free") {
            // Configuration for the free flavor, same syntax as usual
        }
        register("paid") {
            // Configuration for the paid flavor, same syntax as usual
        }
        register("debug") {
            // Configuration for the debug build type, same syntax as usual
        }
        register("release") {
            // Configuration for the release build type, same syntax as usual
        }
    }
}
```

</details>

### Changed
- No changed features!
### Deprecated
- No deprecated features!
### Removed
- The `resDirPath` parameter is no longer needed, since it gets inferred from the flavor or build type configured in the app
### Fixed
- No fixed issues!
### Security
- No security issues fixed!

## [1.0.0] - 2020-07-21
### Added
- Full project refactor in order to improve general stability and reliability of the plug-in.

### Fixed
- The plug-in does not rely on `curl` commands now. 
  Instead it now uses [OkHttp](https://square.github.io/okhttp/) and [Retrofit](https://square.github.io/retrofit/) libraries.
- Tablet strings folder are not generated if no tablet strings are found.

### Changed
- The plugin name to use is now `poEditor` instead of `poEditorPlugin`.
- The input parameters have been changed from snake case to camel case:
```
api_token -> apiToken
project_id -> projectId
default_lang -> defaultLang
res_dir_path -> resDirPath
```

## [0.2.5] - 2016-07-08
### Fixed
- Fix build process to allow integration via JitPack.

## [0.2.4] - 2016-07-08
### Added
- Initial release.

[Unreleased]: https://github.com/bq/poeditor-android-gradle-plugin/compare/1.0.0...HEAD
[1.0.0]: https://github.com/bq/poeditor-android-gradle-plugin/compare/0.2.5...1.0.0
[0.2.5]: https://github.com/bq/poeditor-android-gradle-plugin/compare/v0.2.4...0.2.5
[0.2.4]: https://github.com/bq/poeditor-android-gradle-plugin/releases/tag/v0.2.4
