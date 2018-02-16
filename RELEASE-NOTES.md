## Gradle Native Release Notes

We add noteworthy updates to our [native-samples](https://github.com/gradle/native-samples) and native language support here.

### Changes included in Gradle nightly (next release)

TBD

### Changes included in Gradle 4.6

#410 - We simplified Visual Studio project generation in multi-project builds to create a single solution instead of a solution for every project.
#407 - We refactored the `visual-studio` plugin to make it easier for us to add support for the new C++ plugins.
#209 - We added performance tests for Swift-based builds.
#112 - We added incremental compilation support for Swift.
#422, #421 - We fixed handling of more failure cases for source dependencies.
#151 - We added `sourceCompatibility` for a Swift component. Gradle tries to select the best compiler for producing a given Swift language level.
#195 - We support version range descriptors for source dependencies.
#89 - We support injecting build configuration into a source dependency. Gradle can consume non-Gradle source dependencies by injecting a Gradle build on top.

This list is incomplete.

### Changes included in earlier Gradle releases

gradle-native has been adding features since Gradle 4.1. Features are introduced as `@Incubating` and may change between Gradle minor releases.
