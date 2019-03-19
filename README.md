# easy-qhull

A helper repository to use Qhull in CMake-based C++ projects

## Goal

This repository has been created to make it as easy as possible to use [Qhull](https://github.com/yuki-koyama/easy-qhull) functionality in CMake-based C++ projects.

The specific goal is to allow users to use it simply by `git submodule add ...` and `add_subdirectory(...)`.

## Details

This repository currently uses Qhull 7.3.0.

The `CMakeLists.txt` in this repository defines a target for building Qhull, named `qhull`.

Specifically, `qhull` builds a static library that combines together the two libraries in the original Qhull repository, `libqhullstatic_r` and `libqhullcpp`.

## Example

Suppose that you have a C++ project that looks like
```
$ ls -a
.git
CMakeLists.txt
main.cpp
```

To use `Qhull`, add `easy-qhull` as a git submodule:
```
$ git submodule add https://github.com/yuki-koyama/easy-qhull.git ./external/easy-qhull
$ git submodule update --init --recursive
```

Then, edit `CMakeLists.txt`:
```cmake
...
add_subdirectory(${CMAKE_CURRENT_SOURCE_DIR}/external/easy-qhull)
...
add_executable(my-program ${CMAKE_CURRENT_SOURCE_DIR}/main.cpp)
target_link_libraries(my-program qhull)
...
```

Now you can use `Qhull` functionality in `main.cpp`:
```cpp
#include <libqhullcpp/Qhull.h>

int main()
{
  orgQhull::Qhull qhull;
  qhull.run(...);
  ...
  return 0;
}
```

Finally, this project can be built by a typical CMake cycle, for example,
```
$ cmake . && make
```

## Original Motivation

(TODO)

## Limitations

(TODO)

## Future Work

- Add utility functions to further wrap the Qhull functionality
