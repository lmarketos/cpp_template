cmake_minimum_required(VERSION 3.22)

project(CppSandbox)
add_compile_options(-Wall -Wextra -pedantic -pedantic-errors -Wconversion -Wsign-conversion -Werror)

enable_testing()

add_subdirectory(./src/hello_world)


