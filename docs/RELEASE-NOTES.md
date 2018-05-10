## Gradle Native Release Notes

We add noteworthy updates to our [native-samples](https://github.com/gradle/native-samples) and new [native language support plugins](https://blog.gradle.org/introducing-the-new-cpp-plugins) here.

### Changes included in Gradle nightly (next release)

### Changes included in Gradle 4.8

- Fixed the `cpp-unit-test` plugin so that the dependencies of the main component are visible to the unit test binaries at compile and link time. [#647](https://github.com/gradle/gradle-native/issues/647)
- Fixed the `cpp-unit-test` plugin to allow an application to be tested. Does not yet work on Windows.
- Better control over system include path for native compilation. [#583](https://github.com/gradle/gradle-native/issues/583)

### Changes included in Gradle 4.7

- Converted all of the Swift-related tasks to use the Provider API consistently [#308](https://github.com/gradle/gradle-native/issues/308).
- Added support for declaring the target operating systems for C++/Swift applications and libraries. [#509](https://github.com/gradle/gradle-native/issues/509).
- Added support for Visual Studio solution generation using the `visual-studio` plugin. [#465](https://github.com/gradle/gradle-native/issues/465), [#476](https://github.com/gradle/gradle-native/issues/476), [#506](https://github.com/gradle/gradle-native/issues/506)
- Allow generated Xcode workspace, Visual Studio solution or IDEA project to be opened more easily from the command line. [#553](https://github.com/gradle/gradle-native/issues/553)
- Various Xcode workspace generation fixes. [#474](https://github.com/gradle/gradle-native/issues/474), [#470](https://github.com/gradle/gradle-native/issues/470), [#552](https://github.com/gradle/gradle-native/issues/552)
- Added a [sample](https://github.com/gradle/native-samples#application-uses-a-library-built-by-cmake-cmake-library) that shows how to use libraries built by CMake from Gradle builds.
- Added a [sample](https://github.com/gradle/native-samples#simple-application-application) that shows how to configure the C++ plugins to build C source code, as a workaround until we add C plugins.
- Added a [sample](https://github.com/gradle/native-samples#provisioning-tool-chains-from-within-gradle-provisionable-tool-chains) that shows how to use Gradle to provision a tool chain for the build.
- Fixed Visual Studio version detection to prevent bad Visual Studio installations from failing the build. [#570](https://github.com/gradle/gradle-native/issues/570)
- Made Visual Studio project generation incremental, so only Visual Studio project files that have changed are regenerated. [#506](https://github.com/gradle/gradle-native/issues/506)

### Changes included in Gradle 4.6

- Simplified Visual Studio project generation in multi-project builds to create a single solution instead of a solution for every project. [#410](https://github.com/gradle/gradle-native/issues/410)
- Refactored the `visual-studio` plugin to make it easier for us to add support for the new C++ plugins. [#407](https://github.com/gradle/gradle-native/issues/407)
- Added performance tests for Swift-based builds. [#209](https://github.com/gradle/gradle-native/issues/209)
- Added incremental compilation support for Swift. [#112](https://github.com/gradle/gradle-native/issues/112)
- Fixed handling of more failure cases for source dependencies. [#421](https://github.com/gradle/gradle-native/issues/421) [#422](https://github.com/gradle/gradle-native/issues/422)
- Added `sourceCompatibility` for a Swift component. Gradle tries to select the best compiler for producing a given Swift language level. [#151](https://github.com/gradle/gradle-native/issues/151)
- Support version range descriptors for source dependencies. [#195](https://github.com/gradle/gradle-native/issues/195)
- Support source dependencies on a branch. [#417](https://github.com/gradle/gradle-native/issues/417)
- Support injecting build configuration into a source dependency. Gradle can consume non-Gradle source dependencies by injecting a Gradle build on top. [#89](https://github.com/gradle/gradle-native/issues/89)
- Support generation of a Swift Package Manager manifest file from the Gradle model. [#40](https://github.com/gradle/gradle-native/issues/40)

This list is incomplete.

### Changes included in earlier Gradle releases

gradle-native has been adding features since Gradle 4.1. Features are introduced as `@Incubating` and may change between Gradle minor releases.
