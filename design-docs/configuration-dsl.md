# Tool Chains
> "A tool chain is a set of programming tools that are used to perform a complex software development task or to create a software product, which is typically another computer program or a set of related programs." - Wikipedia

Tool chains consist of a compiler, linker, and libraries. It is possible to mix the preprocessor, compiler and linker of the same toolchain family
(GCC, MSVC and Clang) to produce binaries for the current platform. It's also possible to mix the preprocessor, compiler and
linker between tool chain family (Clang/C2, NASM) to produce binaries for the current platform. When targeting more exotic platform, you can use
preprocessor, compiler, and linker of toolchains for those platforms. It's called cross-compiling. The compiler runs on a host machine targeting an
entirely different architecture and/or operating system. Cross-compilation is all about the linker and sometimes the compiler. It means you could
mix and match preprocessor with other compiler and linker.

Clang family also bring another twist as you can dump the intermediate language (IR), execute transformations on it and feed it back to the backend
of the compiler to complete the compilation. MSVC is moving in this direction as well, and GCC also supports this workflow.

The proposed solution here would be to allow users to access the tool chain resolver more directly as well as enabling them to declare custom tool
chains. Tool chains can be located in the system PATH, at predefined locations, identified from the registry (Windows) or identified through COM
object (Windows), fetched remotely, installed through unattended installers or package manager or manually configured.

## Open Issues
 - The source dialect & ABI is its own beast to support. It's suggested modeling it separately and use compiler version to match variant
 - Should it be named `tool chain` (Gradle) or `toolchain` (Wikipedia)?
 - Should the tool chain and the libraries contained within (prebuilt libraries) be two separate concepts? Meaning the toolchain resolver can be used by prebuilt dependencies but would be tied together.

## DSL

```
toolChainResolvers {
    visualStudio {
        // additional configuration for visual studio resolver
    }
    myCustomResolver(MyCustomResolver) {
        // configuration
    }
}

toolChains {
    myCustomGcc(Gcc) {
        path '...'
    }
    myCustomVisualCpp(VisualCpp) {
        installDir '...'
    }
    myCustomToolChain(ToolChain) {
        tools.add(GccCppCompiler) {
            it.dimensions architectures.x64, operatingSystems.windows
            it.executable = file('/some/other/path')
            it.withArguments { args ->
                args << 'some-arg'
            }
        }

        tools.add(GccLinker) {
            it.dimensions architecture.x64, operatingSystem.windows
            // ...
        }

        installedBy tasks.myCustomToolChainInstallTask

        // TODO - Define how to add libraries
        libraries.add(...) {
            // added libraries can have a...
            //   ...group, e.g. 'com.some.toolchain'
            //   ...name, e.g. 'libc'
            //   ...version (optional), e.g. '2.1'
            // Adding a dependency without a version would depend on the latest or only version declared
        }
    }
}

repositories {
    toolChains.myCustomToolChain
}

dependencies {
    implementation toolChains.myCustomToolChain.libraries.libc
    implementation visualStudio('15.0').libc
}
```

# Build Types

Build types are a conventional dimension for native binaries used to differentiate debug and release version. Additional conventional names
are debug optimized and final. The software model, as well as Android, have this dimension as a first class citizen.
Android typed the items inside their buildTypes container instead of relying on `ext` properties. With the new plugins, the build types will
be typed as well.

## Open Issues

## DSL
```
apply plugin: 'build-types'

buildTypes {
    debug(MyDebugType)
    release(BuildType)
}
```

## Implementations
```
// Common build type
public interface BuildType extends Named {}

// Container type to hold build types
public interface BuildTypeContainer extends ExtensiblePolymorphicDomainObjectContainer<BuildType> {}
```

# Linkage

The linkage container specifies how you want to link your application/library/module together. The static and shared library are simple variants of
the binary.

## Open Issues

* Do we want to specialize the linkage type? For example, `static(MyCustomLinkage)`?

## DSL
```
apply plugin: 'linkage'

linkages {
    // Static library
    static
    // Shared library binary
    shared
    // Compile sources together
    source
    // Executable binary
    executable
}
```

## Implementations
```
public interface Linkage extends Named {}
public interface LinkageContainer extends NamedDomainObjectContainer<Linkage> {}
```

# Prebuilt Libraries
All native dependencies will be using Gradle's dependency management. Due to the complexity of native prebuilt library support, Gradle
will provide a public API for declaring them.

## Open Issues
* Should Gradle allow prebuilt libraries as custom DSL or virtual repository (see example)?

## DSL
Virtual Repository
```
apply plugin: 'boost-cpp'

repositories {
    boost {
        // Configuration allowed by the Boost plugin
    }
}

dependencies {
    // This dependency will ask the `boost` virtual repository where to find Boost:ASIO version 1.63. The repository can look on disk,
    // at a remote location or event checkout the code and build from source.
    implementation group: 'org.boost', name: 'asio', version: '1.63'
}
```

Custom DSL
```
apply plugin: 'boost-cpp'

dependencies {
    // This dependency will provide the right dependency to find Boost:ASIO version 1.63. The dependency element can look on disk,
    // at a remote location or event checkout the code and build from source.
    implementation boost('1.63').asio
}
```


# Instruction Set Architecture (ISA)
The architecture is the interface between the software and hardware. Software written for an ISA can run on different implementations of the same ISA.

## Open Issues
* Do we want to specialize the architecture type? For example, `snesArch(Snes)`.

## DSL
```
architectures {
    x64 {
        pointerSize = 8
        endianness = 'little'
    }
    x86
}
```

# Operating System
```
operatingSystems {
    windows7Sp1(Windows) {
    }
    linux

    customWindows(OperatingSystem) {
        vendor = "Microsoft"
        version = "6.1"
        kernel = "NT"
        distribution = "Windows 7"
    }

    android(OperatingSystem) {
        vendor = "Google"
        version = "7.1.2"
        kernel = "linux"
        distribution = "Android Nougat"
    }

    customMacOS(OperatingSystem) {
        vendor = "Apple"
        version = "10.12.5"
        kernel = "darwin"
        distribution = "macOS Sierra"
    }
}
```

# Dimension Declaration and Filtering
Dimension can be any domain container. It's easy for build author to create new dimensions to fit their needs through custom containers.

## Open Issues
* How should binary variant be declared?
  * Should we explicitly add binaries based on the variant?
  * Alternatively, should we automatically add all variants and explicitly filter out the one we don't want?
  * We could by default add all variant but if you add a single variant explicitly, only the explicit variant would be added.

## DSL
Filtering approach:
```
binaries.dimensions buildTypes, architectures, operatingSystems

// Variant filtering is a chain of closure that gets all executed
binaries.filterVariants {
   if (operatingSystem.windows && architecture.registerSize == 4) {
        ignore()
   }
}
```

Explicit declaration approach:
```
// Add variant through specific elements from dimension containers
binaries.addVariant(linkages.static, buildTypes.debug, operatingSystems.windows)

// Add multiple variant through dimension containers
binaries.addVariant(linkages, buildTypes.matching {it.name.startsWith("debug")}, operatingSystems.windows, architectures)
```

## Implementations
Filtering approach:
```
public interface NativeBinarySpec extends BinarySpec {
    void filterVariants(Action<VariantFilterSpec> configuration);
    void dimensions(NamedDomainObjectContainer containers...);
}

public interface VariantFilterSpec {
    OperatingSystem getOperatingSystem();
    Architecture getArchitecture();
    BuildType getBuildType();
    // General getter for other dimension not tightly integrated

    // Variant selection method
    void ignore();
    void select();

    // Query the filter state from all the filtering action so far
    VariantSelection getState();
}

public enum VariantSelection {
    // A filter explicitly asked to ignore this variant
    EXPLICITLY_IGNORED,

    // A filter explicitly asked to select this variant
    EXPLICITLY_SELECTED,

    // No filter asked for the variant to be ignored or selected
    SELECTED,
}
```

Explicit declaration approach:
```
public interface NativeBinarySpec extends BinarySpec {
    void addVariant(Object dimensions...);
}
```

# Executable DSL
To configure an executable, the user will use the following DSL.

## DSL
```
apply plugin: 'cpp-executable'

executable {
    baseName = 'someName'

    // Configure executable-wide source
    sources {
        cpp {
            // ...
        }
        anotherSource(CppSourceSet) {
            // ...
        }
    }

    binaries.dimensions buildTypes, architectures, operatingSystems

    // Variant filtering is a chain of closure that gets all executed
    binaries.filterVariants {
       if (operatingSystem.windows && architecture.registerSize == 4) {
            ignore()
       }
    }

    binaries.all {
        // configuring all binaries
        cppCompiler.args '-some-args'
        cppPreprocessor.args '-preprocessor'
        [linker, cppCompiler]*.args '-common-args'

    }
    binaries.matching { it.buildType == buildTypes.debug }.all {
        // configure debug binaries only
        sources {
            debugOnlySource(CppSourceSet) {
                // ...
            }
        }
    }
}
```

# Library DSL
## DSL
```
apply plugin: 'cpp-library'

library {
    // Same as `executable`
}
```

# Test suites
Native test suite components should be able to generate binary for both executable and shared linkage as both have executable characteristic.
Some test suite, such as CUnit, doesn't support shared library out-of-the-box. By default, Gradle shouldn't allow it. However, we should be
able to override the decision and make it work.

## DSL
```
apply plugin: 'test-suite'
apply plugin: 'google-test-test-suite'
apply plugin: 'cunit-test-suite'

testSuites {
    aTest(GoogleTestTestSuite) {
        // same as executable DSL
    }
    anotherTest(CUnitTestSuite) {
        // same as executable DSL
    }
    myCustomTest(TestSuite) {
        // same as executable DSL
    }
}
```

# Useful Resources
* https://en.wikipedia.org/wiki/Comparison_of_instruction_set_architectures
