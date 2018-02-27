## Gradle Native Release Notes

We add noteworthy updates to our [native-samples](https://github.com/gradle/native-samples) and new [native language support plugins](https://blog.gradle.org/introducing-the-new-cpp-plugins) here.

### Changes included in Gradle nightly (next release)

- We added support for declaring the target operating systems for C++ applications and libraries. [#465](https://github.com/gradle/gradle-native/issues/509).
- We added support for Visual Studio solution generation using the `visual-studio` plugin. [#465](https://github.com/gradle/gradle-native/issues/465).
- We added a [sample](https://github.com/gradle/native-samples#application-uses-a-library-built-by-cmake-cmake-library) that shows how to use libraries built by CMake from Gradle builds.
- We added a [sample](https://github.com/gradle/native-samples#simple-application-application) that shows how to configure the C++ plugins to build C source code, as a workaround until we add C plugins.

### Changes included in Gradle 4.6

- We simplified Visual Studio project generation in multi-project builds to create a single solution instead of a solution for every project. [#410](https://github.com/gradle/gradle-native/issues/410)
- We refactored the `visual-studio` plugin to make it easier for us to add support for the new C++ plugins. [#407](https://github.com/gradle/gradle-native/issues/407)
- We added performance tests for Swift-based builds. [#209](https://github.com/gradle/gradle-native/issues/209)
- We added incremental compilation support for Swift. [#112](https://github.com/gradle/gradle-native/issues/112)
- We fixed handling of more failure cases for source dependencies. [#421](https://github.com/gradle/gradle-native/issues/421) [#422](https://github.com/gradle/gradle-native/issues/422)
- We added `sourceCompatibility` for a Swift component. Gradle tries to select the best compiler for producing a given Swift language level. [#151](https://github.com/gradle/gradle-native/issues/151)
- We support version range descriptors for source dependencies. [#195](https://github.com/gradle/gradle-native/issues/195)
- We support source dependencies on a branch. [#417](https://github.com/gradle/gradle-native/issues/417)
- We support injecting build configuration into a source dependency. Gradle can consume non-Gradle source dependencies by injecting a Gradle build on top. [#89](https://github.com/gradle/gradle-native/issues/89)
- We support generation of a Swift Package Manager manifest file from the Gradle model. [#40](https://github.com/gradle/gradle-native/issues/40)

This list is incomplete.

### Changes included in earlier Gradle releases

gradle-native has been adding features since Gradle 4.1. Features are introduced as `@Incubating` and may change between Gradle minor releases.
