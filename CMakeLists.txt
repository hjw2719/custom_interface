cmake_minimum_required(VERSION 3.5)
project(interface)

#list(APPEND CMAKE_MODULE_PATH ${CMAKE_BINARY_DIR})
#list(APPEND CMAKE_PREFIX_PATH ${CMAKE_BINARY_DIR})

# Default to C99
if(NOT CMAKE_C_STANDARD)
  set(CMAKE_C_STANDARD 99)
endif()

# Default to C++14
if(NOT CMAKE_CXX_STANDARD)
  set(CMAKE_CXX_STANDARD 14)
endif()

if(CMAKE_COMPILER_IS_GNUCXX OR CMAKE_CXX_COMPILER_ID MATCHES "Clang")
  add_compile_options(-Wall -Wextra -Wpedantic)
endif()

#if(NOT EXISTS "${CMAKE_BINARY_DIR}/conan.cmake")
#  message(STATUS "Downloading conan.cmake from https://github.com/conan-io/cmake-conan")
#  file(DOWNLOAD "https://raw.githubusercontent.com/conan-io/cmake-conan/v0.16.1/conan.cmake"
#                "${CMAKE_BINARY_DIR}/conan.cmake"
#                EXPECTED_HASH SHA256=396e16d0f5eabdc6a14afddbcfff62a54a7ee75c6da23f32f7a31bc85db23484
#                TLS_VERIFY ON)
#endif()

#include(${CMAKE_BINARY_DIR}/conan.cmake)
#message("====== ${CMAKE_BINARY_DIR}")


# find dependencies
find_package(ament_cmake REQUIRED)
# uncomment the following section in order to fill in
# further dependencies manually.
# find_package(<dependency> REQUIRED)
find_package(rosidl_default_generators REQUIRED)
find_package(std_msgs REQUIRED)
rosidl_generate_interfaces(${PROJECT_NAME}
  "msg/Num.msg"
  "msg/Hsc4.msg"
  DEPENDENCIES
  std_msgs
 )

ament_export_dependencies(rosidl_default_runtime)

#message(STATUS "${CONAN_FIND_PACKAGE_DIR} ================")
#conan_cmake_run(
#    CONANFILE conanfile.py
#    INSTALL_FOLDER ${CONAN_FIND_PACKAGE_DIR}
#    SETTINGS compiler.libcxx=libstdc++
#    SETTINGS arch=${CMAKE_SYSTEM_PROCESSOR}
#    BUILD_TYPE Release
#)

if(BUILD_TESTING)
  find_package(ament_lint_auto REQUIRED)
  # the following line skips the linter which checks for copyrights
  # uncomment the line when a copyright and license is not present in all source files
  #set(ament_cmake_copyright_FOUND TRUE)
  # the following line skips cpplint (only works in a git repo)
  # uncomment the line when this package is not in a git repo
  #set(ament_cmake_cpplint_FOUND TRUE)
  ament_lint_auto_find_test_dependencies()
endif()

ament_package()
