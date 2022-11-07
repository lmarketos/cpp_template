cmake_minimum_required(VERSION 3.22)

project(CppSandbox)
add_compile_options(-Werror -Wall -Wextra -Wconversion -pedantic -pedantic-errors -Wconversion -Wsign-conversion)

enable_testing()

add_subdirectory(./src/hello_world)


