add_custom_target(PerfTests)
set_target_properties(PerfTests PROPERTIES FOLDER "Tests")

# Xcode perftests use Objective-C++ and link to llbuild C++ libs. They require Clang
# (GCC doesn't support ObjC++). Building .mm with Clang and linking to GCC-built libs
# would mix libc++ and libstdc++, so we skip Xcode perftests when using GCC.
if(CMAKE_SYSTEM_NAME MATCHES "Darwin" AND NOT CMAKE_CXX_COMPILER_ID STREQUAL "GNU")
  add_subdirectory(Xcode/PerfTests)
endif()
