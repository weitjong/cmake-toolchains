# cmake-1

**cmake-1** is a collection of CMake modules and toolchains for cross-compiling. The collection was originally developed as part of [Urho3D](https://urho3d.github.io/) project, a cross-platform 2D and 3D game engine, before being hosted separately here to cater for more general use case by other CMake-based projects. 

## License

Licensed under the MIT license, see [LICENSE](https://github.com/weitjong/cmake-1/blob/master/LICENSE) for details.

## Installation

Download or git clone the **cmake-1** repository to the root of your project source tree as `cmake-1` subdir.

```bash
cd /path/to/your/project/source/tree/
git clone https://github.com/weitjong/cmake-1.git
```

## Module usage

Add the `cmake-1/Modules` subdir as one of the CMake module search path in your project main `CMakeLists.txt` file.

```bash
set (CMAKE_MODULE_PATH ${CMAKE_SOURCE_DIR}/cmake-1/Modules)
```

Most of the module files for the `find_package()` command will be auto-included by CMake when they are needed. For other types of module files, however, you have to use the `include()` command to include them explicitly in your script.

## Toolchain usage

Set a convenient environment variable to point to the `cmake-1/Toolchain` subdir and use the environment variable when invoking **cmake** CLI or GUI with the `-DCMAKE_TOOLCHAIN_FILE` option; or use the environment variable in your helper shell script or batch file which does the invoking.

### Bash script

```bash
export SOURCE=/path/to/your/project/source/tree
export BUILD=/path/to/your/project/build/tree

export TOOLCHAINS="$SOURCE"/cmake-1/Toolchains
export OPTS="-DCMAKE_TOOLCHAIN_FILE=$TOOLCHAINS/Emscripten.cmake"

cmake -E make_directory "$BUILD" && cmake -E chdir "$BUILD" cmake $OPTS $@ "$SOURCE"

```

### Batch file

```bash
set "SOURCE=\path\to\your\project\source\tree"
set "BUILD=\path\to\your\project\build\tree"

set "TOOLCHAINS=%SOURCE%\cmake-1\Toolchains"
set "OPTS=-DCMAKE_TOOLCHAIN_FILE="%TOOLCHAINS%\Emscripten.cmake""

cmake -E make_directory "%BUILD%" && cmake -E chdir "%BUILD%" cmake %OPTS% %* "%SOURCE%"
```

Note that the `Emscripten.cmake` is just one of the available toolchain files. You can substitute it with other toolchain file provided by **cmake-1**.
