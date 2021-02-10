This is a Gradle plugin for integrating Project Panama's [`jextract`](http://cr.openjdk.java.net/~mcimadamore/panama/jextract_distilled.html) tool in the build process.

## :bulb: &nbsp; Example

Since the plugin is available on [Gradle's Plugin Portal](https://plugins.gradle.org/) it can be applied within the build script's `plugins` block.

```gradle
plugins {
  id "io.github.krakowski.jextract" version "0.1.5"
}
```

Applying the plugin adds the `jextract` task which can be configured by the build script.

```gradle
jextract {
    // The library name
    libraries = [ 'stdc++' ]

    // The package under which all source files will be generated
    targetPackage = 'org.unix'

    // The header file jextract should parse
    header = "${project.projectDir}/src/main/c/stdio.h"
}
```

## :triangular_ruler: &nbsp; Configuration Options

The `jextract` task exposes the following configuration options.

|       Name       |               Type              |    Required    | Description                                                                     |
|:----------------:|:-------------------------------:|:--------------:|---------------------------------------------------------------------------------|
| `clangArguments` |        `java.lang.String`       |                | Arguments which should be passed to clang                                       |
|   `libraries`    |       `java.lang.String[]`      | :black_circle: | The libraries against which the native code will link                           |
|  `targetPackage` |        `java.lang.String`       | :black_circle: | The package under which all bindings will be generated                          |
|    `includes`    |       `java.lang.String[]`      |                | A list of directories which should be included during code generation           |
|     `header`     |        `java.lang.String`       | :black_circle: | The header file jextract should parse                                           |
|    `filters`     |       `java.lang.String[]`      |                | Whitelist for header files. Checks absolute paths for existence of substring    |
|   `sourceMode`   |       `java.lang.Boolean`       |                | Generate source files instead of class files                                    |
|    `outputDir`   | `org.gradle.api.file.Directory` |                | The output directory under which the generated source files will be placed      |

## :wrench: &nbsp; Requirements

  * [OpenJDK 17 + Project Panama](https://github.com/openjdk/panama-foreign/tree/foreign-jextract)
  * [LLVM 9+](https://releases.llvm.org/download.html)
  
## :scroll: &nbsp; License

This project is licensed under the GNU GPLv3 License - see the [LICENSE](LICENSE) file for details.