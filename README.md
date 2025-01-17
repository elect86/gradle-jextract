This is a Gradle plugin for integrating Project Panama's [`jextract`](http://cr.openjdk.java.net/~mcimadamore/panama/jextract_distilled.html) tool in the build process.

## :bulb: &nbsp; Example

Since the plugin is available on [Gradle's Plugin Portal](https://plugins.gradle.org/) it can be applied within the build script's `plugins` block.

```gradle
plugins {
  id "io.github.krakowski.jextract" version "0.1.6"
}
```

Applying the plugin adds the `jextract` task which can be configured by the build script.

```gradle
jextract {

    fromHeader("${project.projectDir}/src/main/c/stdio.h)= {
        // The library name
        libraries = [ 'stdc++' ]
    
        // The package under which all source files will be generated
        targetPackage = 'org.unix'
        
        // The generated class name
        className = 'Linux'
    }
}
```

There is also a [full demo project](https://github.com/krakowski/jextract-demo) showcasing the `gradle-jextract` plugin.

## :triangular_ruler: &nbsp; Configuration Options

The `jextract` task exposes the following configuration options.

|       Name       |               Type              |    Required    | Description                                                                |
|:----------------:|:-------------------------------:|:--------------:|----------------------------------------------------------------------------|
| `clangArguments` |        `java.lang.String`       |                | Arguments which should be passed to clang                                  |
|    `libraries`   |       `java.lang.String[]`      | :black_circle: | The libraries against which the native code will link                      |
|    `includes`    |       `java.lang.String[]`      |                | A list of directories which should be included during code generation      |
|  `targetPackage` |        `java.lang.String`       | :black_circle: | The package under which all bindings will be generated                     |
|    `className`   |        `java.lang.String`       |                | The generated class file's name                                            |
|    `functions`   |       `java.lang.String[]`      |                | Whitelist of function symbols                                              |
|     `macros`     |       `java.lang.String[]`      |                | Whitelist of macro symbols                                                 |
|     `structs`    |       `java.lang.String[]`      |                | Whitelist of struct symbols                                                |
|    `typedefs`    |       `java.lang.String[]`      |                | Whitelist of typedef symbols                                               |
|     `unions`     |       `java.lang.String[]`      |                | Whitelist of union symbols                                                 |
|    `variables`   |       `java.lang.String[]`      |                | Whitelist of global variable symbols                                       |
|   `sourceMode`   |       `java.lang.Boolean`       |                | Generate source files instead of class files                               |
|    `outputDir`   | `org.gradle.api.file.Directory` |                | The output directory under which the generated source files will be placed |

## :wrench: &nbsp; Requirements

  * [OpenJDK 17 + Project Panama](https://github.com/openjdk/panama-foreign/tree/foreign-jextract)
  * [LLVM 9+](https://releases.llvm.org/download.html)

## :warning: &nbsp; Known issues

- Gradle is often incompatible with newly released Java versions, resulting in the error message `Unsupported class file major version`. The `gradle-jextract` plugin can work around this by using a different JDK for compiling the sources. To enable this feature the `javaHome` property has to be set within your global `gradle.properties` usually located inside `${HOME}/.gradle`.

  ```
  javaHome=/path/to/your/panama/java/home
  ```
  
## :scroll: &nbsp; License

This project is licensed under the GNU GPLv3 License - see the [LICENSE](LICENSE) file for details.