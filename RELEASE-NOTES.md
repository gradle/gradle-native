## Gradle Native Release Notes

We add noteworthy updates to our [native-samples](https://github.com/gradle/native-samples) and native language support here.

### Changes included in Gradle nightly (next release)

TBD

### Changes included in Gradle 4.6

- We simplified Visual Studio project generation in multi-project builds to create a single solution instead of a solution for every project. #410
- We refactored the `visual-studio` plugin to make it easier for us to add support for the new C++ plugins. #407
- We added performance tests for Swift-based builds. #209
- We added incremental compilation support for Swift. #112
- We fixed handling of more failure cases for source dependencies. #422, #421
- We added `sourceCompatibility` for a Swift component. Gradle tries to select the best compiler for producing a given Swift language level. #151
- We support version range descriptors for source dependencies. #195
- We support injecting build configuration into a source dependency. Gradle can consume non-Gradle source dependencies by injecting a Gradle build on top. #89

This list is incomplete.

### Changes included in earlier Gradle releases

gradle-native has been adding features since Gradle 4.1. Features are introduced as `@Incubating` and may change between Gradle minor releases.
