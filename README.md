# gradle-native

The home of Gradle's support for natively compiled languages. 

## Latest updates

You can track [closed issues](https://github.com/gradle/gradle-native/issues?q=is%3Aissue+is%3Aclosed) and our regular updates in our [release notes](docs/RELEASE-NOTES.md).

We have a [`#native` Slack channel](https://gradle-community.slack.com/archives/CA7UM03V3/p1539291588000100) on the [Gradle Community Slack](https://discuss.gradle.org/t/introducing-gradle-community-slack/26731).

## What is gradle-native?

As of 4.1, Gradle includes several plugins for building applications and libraries from C++ and Swift sources. Check out the [blog post](https://blog.gradle.org/introducing-the-new-cpp-plugins) for an introduction.

- Issues related to Gradle's support for native languages are tracked in this repo.
- This repository also includes some [WIP documentation](docs/README.md) and [release notes](docs/RELEASE-NOTES.md)
- Samples are in the [native-samples](https://github.com/gradle/native-samples) repo.
- The source code for the plugins still lives in the [gradle](https://github.com/gradle/gradle) repo and will migrate here over time.

For more information about Gradle, please visit: https://gradle.org

This project adheres to the [Gradle Code of Conduct](https://gradle.org/conduct/). By participating, you are expected to uphold this code.

## Features

- Compile and link libraries and applications from C++ and Swift source.
- Build C++ for macOS, Linux and Windows.
- Build Swift for macOS and Linux.
- Supports GCC, Clang, Visual C++, MinGW compilers.
- Fast parallel, incremental compilation for C++.
- Incremental compilation for Swift.
- Distributed caching of C++ and Swift compilation.
- Transitive dependency management, including support for composite builds and pre-built binaries from a Maven binary repository. Other pre-built binaries are not yet supported.
- Source dependencies.
- Publishing dependencies to a Maven binary repository.
- Tool chain discovery based on requirements declared in the build, including discovery of these compilers when running on cygwin or using Visual C++.
- Xcode integration, to allow you to generate Xcode workspace and project files from your Gradle build.
- Visual Studio integration, to allow you to generate a Visual Studio solution and project files from your Gradle build.
- XCTest integration, supported on macOs and Linux.

## Contributing

If you're looking to contribute to Gradle or provide a patch/pull request, you can find more info [here](https://github.com/gradle/gradle-native/blob/master/.github/CONTRIBUTING.md).
