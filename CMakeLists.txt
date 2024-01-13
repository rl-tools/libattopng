cmake_minimum_required(VERSION 2.8.9)
project(libattopng)

add_library(libattopng include/libattopng.c)
target_include_directories(libattopng PUBLIC include)

add_executable(libattopng test.c libattopng.c) 
target_link_libraries(libattopng)


# install

install(TARGETS libattopng DESTINATION lib)
install(FILES include/libattopng.h DESTINATION include)
 
