# cpp_template
Sample project with build and unit test support. Self-contained environment for building/testing through the use of a build environment docker.

Intended to be cloned or used as a template for a starting point for home C++ projects.

## Getting started
From the root directory of the repo:

Build the docker image used to compile the application and run analysis tools
```
./dev build_docker
```
Build the sample application
```
./dev build
```
Run the sample application
```
./bin/HelloWorld
```    
Run a bash shell in the build docker
```
./dev shell
```
## To Do
 - switch user in docker commands to prevent files being written as root
 - add unit test
 - run unit test
 - set build options
 - set clang build
 - set gcc build
 - run clang-tidy
 - run cppcheck
 - hooks for clang-format
