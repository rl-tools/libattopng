cmake_minimum_required(VERSION 2.8.9)
project(libattopng)

add_library(libattopng libattopng.c)
target_include_directories(
        libattopng PUBLIC
        $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include>
        $<INSTALL_INTERFACE:include>
)

add_executable(libattopng_test test.c)
target_link_libraries(libattopng_test libattopng)


# install

install(
        TARGETS libattopng
        EXPORT libattopng_Targets
        ARCHIVE DESTINATION lib
        LIBRARY DESTINATION lib
        INCLUDES DESTINATION include
)
install(
        EXPORT libattopng_Targets
        FILE libattopngTargets.cmake
        NAMESPACE libattopng::
        DESTINATION lib/cmake/libattopng
)
install(
        FILES "${CMAKE_CURRENT_BINARY_DIR}/libattopngConfig.cmake"
        DESTINATION lib/cmake/libattopng
)
include(CMakePackageConfigHelpers)
configure_package_config_file(
        "${CMAKE_CURRENT_SOURCE_DIR}/cmake/libattopngConfig.cmake.in"
        "${CMAKE_CURRENT_BINARY_DIR}/libattopngConfig.cmake"
        INSTALL_DESTINATION lib/cmake/libattopng
)
install(DIRECTORY ${PROJECT_SOURCE_DIR}/include/ DESTINATION include)
#install(DIRECTORY include/ DESTINATION include)

