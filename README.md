# cpp_template
Sample project with build and unit test support. Self-contained environment for building/testing through the use of a build environment docker.

Intended to be cloned or used as a template for a starting point for home C++ projects.

## Getting started
From the root directory of the repo:

Build the docker image used to compile the application and run analysis tools
```
./dev build_docker
```
Build the sample application. Note that the docker mounts the root dir of the repo so files are never copied into the build docker. You can edit your source locally in the repo
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
For a complete list of options
```
./dev -h
```
## To Do
 - add unit test
 - run unit test
 - set build options
 - set clang build
 - set gcc build
 - run clang-tidy
 - run cppcheck
 - hooks for clang-format
