class: center, middle

# CMake von Hello World nach…

---

# Agenda

* CMake

* Hello World

* Dependencies mit find_package und xyzConfig.cmake

???
* Notizen hier


---

# CMake

* Cross Platform Build System
* Generiert Native Projekte (Make, Ninja, Xcode, Visual Studio)
* Unterstützt Abhängihkeiten und Modularisierung
* Gute Untestützung für Qt 5

Was ist CMake?

* CMake: cmake, ccmake, cmake-gui
* CTest: ctest
* CPack cpack
* http://www.cmake.org/
* http://www.cmake.org/documentation/

---

# CMake mit einer Datei

```cpp
int main() {
  std::cout << "Hello World" << std::endl;
  return 0;
}
```

```cmake
cmake_minimum_required( VERSION 3.1 )
project( example1 )

add_executable( hello main.cpp )
install( TARGETS hello DESTINATION bin )
```

```sh
mkdir build  && cd build
cmake -DCMAKE_BUILD_TYPE=Release ..
make install
```

---

# CMake mit mehreren Dateien

* `CMakeLists.txt`
* `main.cpp`
* `print.cpp`
* `print.hpp`

```cpp
*#include "print.hpp"

int main() {
  print();
  return 0;
}
```

```cmake
...
add_executable( hello
  main.cpp
  print.cpp
  print.hpp    ## optional, included for IDE
)
```

---

# CMake mit eigenen Libraries

* `CMakeLists.txt`
* `main.cpp`
* `libprint/`
  * `CMakeLists.txt`
  * `print.hpp`
  * `print.cpp`


```cpp
*#include <print.hpp>

int main() {
  print();
  return 0;
}
```

---

# CMake mit eigenen Libraries (2)

```cmake
cmake_minimum_required(VERSION 3.1)
project( example1 )

add_subdirectory( libprint )

add_executable( hello main.cpp )
*target_link_libraries( hello print )
install( TARGETS hello DESTINATION bin )
```

```cmake
add_library( print STATIC
  print.cpp
  print.hpp
)
*target_include_directories( print PUBLIC ${CMAKE_CURRENT_SOURCE_DIR} )
```
