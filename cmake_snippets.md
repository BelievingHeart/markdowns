[//]: # (#cmake snippets)
## cmake version requirement
[Link](https://cliutils.gitlab.io/modern-cmake/chapters/basics.html)
```cmake
cmake_minimum_required(VERSION 3.1...3.12)

if(${CMAKE_VERSION} VERSION_LESS 3.12)
  cmake_policy(VERSION ${CMAKE_MAJOR_VERSION}.${CMAKE_MINOR_VERSION})
endif()
```

## protect against building in project src root
```cmake
if(${PROJECT_SOURCE_DIR} STREQUAL ${PROJECT_BINARY_DIR})
    message(FATAL_ERROR "In-source builds not allowed. Please make a new directory (called a build directory) and run CMake from there.")
endif()
```

## standard build dirs
```cmake
include(GNUInstallDirs)
set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/${CMAKE_INSTALL_LIBDIR})
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/${CMAKE_INSTALL_LIBDIR})
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/${CMAKE_INSTALL_BINDIR})
```

## standard install dirs
```cmake
set(INSTALL_LIBDIR ${CMAKE_INSTALL_LIBDIR} CACHE PATH "Installation directory for libraries")
set(INSTALL_BINDIR ${CMAKE_INSTALL_BINDIR} CACHE PATH "Installation directory for executables")
set(INSTALL_INCLUDEDIR ${CMAKE_INSTALL_INCLUDEDIR} CACHE PATH "Installation directory for header files")
if(WIN32 AND NOT CYGWIN)
  set(DEF_INSTALL_CMAKEDIR CMake)
else()
  set(DEF_INSTALL_CMAKEDIR share/cmake/${PROJECT_NAME})
endif()
set(INSTALL_CMAKEDIR ${DEF_INSTALL_CMAKEDIR} CACHE PATH "Installation directory for CMake files")
```

## rpath from runtime to shared lib
```cmake
file(RELATIVE_PATH _rel ${CMAKE_INSTALL_PREFIX}/${INSTALL_BINDIR} ${CMAKE_INSTALL_PREFIX}/${INSTALL_LIBDIR})
if(APPLE)
  set(_rpath "@loader_path/${_rel}")
else()
  set(_rpath "\$ORIGIN/${_rel}")
endif()
```

## frequent template
```cmake
cmake_minimum_required(VERSION 3.12)
project(hello)


set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

#set(CMAKE_LINK_WHAT_YOU_USE TRUE)
#find_program(TIDY "clang-tidy-6.0")
#set(CMAKE_CXX_CLANG_TIDY ${TIDY} "-checks=*")
#find_program(CPPCHECK cppcheck "--std=c++14")
#set(CMAKE_CXX_CPPCHECK ${CPPCHECK})
#find_program(IWYU include-what-you-use)
#set(CMAKE_CXX_INCLUDE_WHAT_YOU_USE  ${IWYU})

find_package(fmt REQUIRED CONFIG)
find_package(OpenCV REQUIRED)
add_executable(main main.cpp)
target_include_directories(main PRIVATE ${OpenCV_INCLUDE_DIRS})
target_link_libraries(main PRIVATE ${OpenCV_LIBS} fmt::fmt)
if(CMAKE_BUILD_TYPE MATCHES Debug)
    target_compile_definitions(main PRIVATE DEBUG)
endif()
```