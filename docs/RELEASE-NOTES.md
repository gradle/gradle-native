# Gradle Native Release Notes

We add noteworthy updates to our [native-samples](https://github.com/gradle/native-samples) and new [native language support plugins](https://blog.gradle.org/introducing-the-new-cpp-plugins) here.

## Changes included in Gradle nightly (next release)

## Changes included in Gradle 6.0

- New C++ and Swift plugins are deincubated
- Visual Studio generated IDE files honors the `/std:c++14` and `/std:c++latest` compiler flags for IntelliSense
- Visual Studio 2019 compilers are officially supported

## Changes included in Gradle 5.6

- Support XCTest's `LinuxMain.swift` pattern - [PR](https://github.com/gradle/gradle/pull/9680)
- Swift documentations have been released

## Changes included in Gradle 5.5

- All native documentations have been updated to use the new C++ plugins

## Changes included in Gradle 5.4

- Fix native test plugins when application has multiple target machines - [PR](https://github.com/gradle/gradle/pull/8819)
- C++ compile tasks complete with `NO-SOURCE` when no compilation units are present - [PR](https://github.com/gradle/gradle/pull/8815)
- Official support for Swift 5 language released with Xcode 10.2 - [PR](https://github.com/gradle/gradle/pull/8852)

## Changes included in Gradle 5.2

- Official support for GCC with Cygwin64 - [#127](https://github.com/gradle/gradle-native/issues/127)
- Official support for GCC with MinGW64 - [#419](https://github.com/gradle/gradle-native/issues/419)
- Gradle emits a warning message when trying to build a project that does not target the host operating system - [#929](https://github.com/gradle/gradle-native/issues/929)
- Gradle now relocates the main symbol in applications, so they can be tested like libraries - [community PR](https://github.com/gradle/gradle/pull/8127).
- Gradle's `init` task can now generate C++ application and library sample projects.

## Changes included in Gradle 5.1

- Incremental compile processor takes preprocessor macros declared on the compile task into account - [#882](https://github.com/gradle/gradle-native/issues/882)
- Support for declaring different architecture targets (x86, x86-64) - [#777](https://github.com/gradle/gradle-native/issues/777)

## Changes included in Gradle 5.0

Since 4.0, the Gradle team have been hard at work improving support for native projects in Gradle.

First and foremost, Gradle formed a team to tackle all native related issues and development. We created a separate issue tracker ([`gradle/gradle-native`](https://github.com/gradle/gradle-native)) and a dedicated `native` tag on the [user forum](https://discuss.gradle.org).

We [announced our focus shift from the software model to the current configuration model](https://blog.gradle.org/state-and-future-of-the-gradle-software-model) to make developing native projects more similar to existing Java, Groovy and Scala plugins. This led to the development of the [new C++ plugins](https://blog.gradle.org/introducing-the-new-cpp-plugins) that are used throughout our [use-case focused samples](https://github.com/gradle/native-samples).

Those new C++ plugins are still experimental but will eventually replace the software model based C++ plugins.

During the 4.x releases, we made changes to Visual Studio solution generation to make it easier to work with multi-project builds in Visual Studio. We also introduce support for developing C++ with the Xcode IDE on macOS. JetBrains integrated support for [importing and syncing Gradle projects](https://www.jetbrains.com/help/clion/gradle-support.html) into Clion.

We expanded our tool chain support to include Visual Studio 2017 together with Windows 10 SDK.

We improved performance by supporting parallel execution for compilation and linking.  We also support for cached [compilation](https://docs.gradle.org/4.5/release-notes.html#c/c++-compilation-improvements). With the new C++ plugins, it is possible to unit test a C++ application right out-of-the-box.

We recently [introduced source dependencies](https://blog.gradle.org/introducing-source-dependencies), which allow any Gradle project (native or not) to build against a git repository.

### Bugfixes
- C++ compilation uses correct system includes files on Cygwin - [#763](https://github.com/gradle/gradle-native/issues/763)
- Improve performance for header analysis when external macros are defined - [#882](https://github.com/gradle/gradle-native/issues/882)

## Changes included in Gradle 4.10

- C++ tooling API model that IDEs can use for import or sync - [#673](https://github.com/gradle/gradle-native/issues/673)
- Source dependencies honor the `--offline` flag - [#430](https://github.com/gradle/gradle-native/issues/430)
- Source dependencies reduce remote Git operations - [#403](https://github.com/gradle/gradle-native/issues/403)

## Changes included in Gradle 4.9

### Bugfixes

- Fixed text rendering issues in console that caused output from long running tasks to be broken by tasks that produced no output [#669](https://github.com/gradle/gradle-native/issues/669)
- XCTest succeeds when it should fail - [#378](https://github.com/gradle/gradle-native/issues/378)

## Changes included in Gradle 4.8

### Expose main C++ component to unit test binary - [#647](https://github.com/gradle/gradle-native/issues/647)

The `cpp-unit-test` plugin was fixed so that the dependencies of the main component are visible to the unit test binaries at compile and link time. 

### Allow C++ application to be tested

The `cpp-unit-test` plugin will automatically relocate the main symbol to avoid duplicate `_main` symbol errors.
Note this feature is not yet supported on Windows.

### Performance improvements for header analysis

Gradle will reuse header analysis from the previous execution if nothing has changed.

### Better control over system include path for native compilation - [#583](https://github.com/gradle/gradle-native/issues/583)

In previous versions of Gradle, the native compile task include path was a single monolithic collection of files that was accessible through the `includes` property on the compile task.
In Gradle 4.8, system header include directories can now be accessed separately via the `systemIncludes` property. 
On GCC-compatible toolchains, the system header include directories specified with `systemIncludes` will be specified on the command line using the ["-isystem" argument](https://gcc.gnu.org/onlinedocs/gcc/Directory-Options.html), which marks them for special treatment by the compiler.

## Changes included in Gradle 4.7

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

## Changes included in Gradle 4.6

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

## Changes included in earlier Gradle releases

gradle-native has been adding features since Gradle 4.1. Features are introduced as `@Incubating` and may change between Gradle minor releases.
