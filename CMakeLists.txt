cmake_minimum_required(VERSION 3.15)
project(opencv_test CXX)

find_package(OpenCV REQUIRED core CONFIG)

add_executable(opencv_test src/test_photo.cpp)

target_link_libraries(opencv_test PRIVATE opencv_photo)

install(TARGETS opencv_test DESTINATION "."
        RUNTIME DESTINATION bin
        ARCHIVE DESTINATION lib
        LIBRARY DESTINATION lib
        )
