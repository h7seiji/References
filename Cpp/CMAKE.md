# CMAKE

CMake is a powerful cross-platform build system that generates build files, Makefiles, or workspaces for various platforms and compilers.
Unlike the others build systems, CMake does not actually build the project, it only generates the files needed by build tools.
CMake is widely used, particularly in C++ projects, for its ease of use and flexibility.

## CMakeLists.txt

CMake uses a file called `CMakeLists.txt` to define settings, source files, libraries, and other configurations.
A typical CMakeLists.txt for a simple project would look like:

```cpp
cmake_minimum_required(VERSION 3.0)

project(MyProject)

set(SRC_DIR "${CMAKE_CURRENT_LIST_DIR}/src")
set(SOURCES "${SRC_DIR}/main.cpp" "${SRC_DIR}/file1.cpp" "${SRC_DIR}/file2.cpp")

add_executable(${PROJECT_NAME} ${SOURCES})

target_include_directories(${PROJECT_NAME} PRIVATE "${CMAKE_CURRENT_LIST_DIR}/include")

set_target_properties(${PROJECT_NAME} PROPERTIES
    CXX_STANDARD 14
    CXX_STANDARD_REQUIRED ON
    CXX_EXTENSIONS OFF
)
```

## Building with CMake

Here is an example of a simple build process using CMake:

1. Create a new directory for the build.

```bash
mkdir build
cd build
```

2. Generate build files using CMake.

```bash
cmake ..
```

3. Build the project using the generated build files.

```bash
make
```

Or, on Windows with Visual Studio, you may use:

```bash
msbuild MyProject.sln
```
