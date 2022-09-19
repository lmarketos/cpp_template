
add_executable(HelloWorld main.cpp)

install(TARGETS HelloWorld DESTINATION bin)

enable_testing()
list(APPEND CMAKE_PREFIX_PATH "/usr/lib/x86_64-linux-gnu/cmake/GTest")
find_package(GTest REQUIRED)

add_executable(hello_test test/hello_test.cpp)
target_link_libraries(hello_test GTest::gtest_main)

add_test(NAME example_test COMMAND hello_test)
