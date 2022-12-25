cmake_minimum_required(VERSION 3.12.4)

set(PATCH_VERSION "1" CACHE INTERNAL "Patch version")
set(PROJECT_VESRION 0.0.${PATCH_VERSION})

project(hw5_matrix VERSION ${PROJECT_VESRION})

set(CMAKE_CXX_STANDARD 17)

include(FetchContent)
FetchContent_Declare(
        googletest
        # Specify the commit you depend on and update it regularly.
        URL https://github.com/google/googletest/archive/5376968f6948923e2411081fd9372e71a59d8e77.zip
)
# For Windows: Prevent overriding the parent project's compiler/linker settings
set(gtest_force_shared_crt ON CACHE BOOL "" FORCE)
FetchContent_MakeAvailable(googletest)

find_package (Threads REQUIRED)

add_executable(matrix main.cpp matrix.cpp)
add_library(matrix.lib STATIC lib.cpp)
#add_executable(test_google test.cpp)

target_include_directories(matrix.lib
    PUBLIC "${CMAKE_BINARY_DIR}"
)

target_link_libraries(matrix
    matrix.lib
)

#target_link_libraries(test_google
#    gtest
#    ${CMAKE_THREAD_LIBS_INIT}
#)

install(TARGETS matrix RUNTIME DESTINATION bin)

set(CPACK_GENERATOR DEB)
set(CPACK_PACKAGE_VERSION_MAJOR "${PROJECT_VERSION_MAJOR}")
set(CPACK_PACKAGE_VERSION_MINOR "${PROJECT_VERSION_MINOR}")
set(CPACK_PACKAGE_VERSION_PATCH "${PROJECT_VERSION_PATCH}")
set(CPACK_PACKAGE_CONTACT example@example.com)
include(CPack)

#enable_testing()
#add_test(GOOGLE_TEST1 matrix)
#add_test(GOOGLE_TEST2 matrix)
#add_test(GOOGLE_TEST3 matrix)
