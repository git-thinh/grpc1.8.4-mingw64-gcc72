msys2 (with mingw)

The Makefile (and source code) should support msys2's mingw32 and mingw64 compilers. Building with msys2's native compiler is also possible, but difficult.

This approach requires having msys2 installed.

# Install prerequisites

MSYS2$ pacman -S autoconf automake gcc libtool mingw-w64-x86_64-toolchain perl pkg-config zlib
MSYS2$ pacman -S mingw-w64-x86_64-gflags

MSYS2$ git clone https://github.com/grpc/grpc.git
MSYS2$ cd grpc/


# From mingw shell

MSYS2$ export CPPFLAGS="-D_WIN32_WINNT=0x0600"
MSYS2$ make

NOTE: While most of the make targets are buildable under Mingw, 
ome haven't been ported to Windows yet and may fail to build 
(mostly trying to include POSIX headers not available on Mingw).

Package zlib was not found in the pkg-config search path.
Perhaps you should add the directory containing `zlib.pc'
to the PKG_CONFIG_PATH environment variable
No package 'zlib' found
Package libcares was not found in the pkg-config search path.
Perhaps you should add the directory containing `libcares.pc'
to the PKG_CONFIG_PATH environment variable
No package 'libcares' found

DEPENDENCY ERROR

You are missing system dependencies that are essential to build grpc,
and the third_party directory doesn't have them:

  zlib cares

Installing the development packages for your system will solve
this issue. Please consult INSTALL to get more information.

If you need information about why these tests failed, run:

  make run_dep_checks

Additionally, since you are in a git clone, you can download the
missing dependencies in third_party by running the following command:

  git submodule update --init

make: *** [Makefile:946: stop] Error 1


MSYS2$ git submodule update --init
MSYS2$ make run_dep_checks
pkg-config --atleast-version=1.0.2 openssl || true
pkg-config --atleast-version=1.0.1 openssl || true
pkg-config --exists zlib || true
cc -Ithird_party/protobuf/src -Ithird_party/googletest/googletest/include -Ithird_party/googletest/googlemock/include -Ithird_party/boringssl/include -Ithird_party/cares -Ithird_party/cares/cares -D_WIN32_WINNT=0x0600 -g -Wall -Wextra -Werror -Wno-long-long -Wno-unused-parameter -DOSATOMIC_USE_INLINED=1 -Wno-deprecated -declarations -O2 -I. -Iinclude -I/home/MrThinh/grpc/gens -DNDEBUG -DINSTALL_PREFIX=\"/usr/local\"   -Ithird_party/zlib -std=c99 -Wsign-conversion -Wconversion -Wshadow    -o `mktemp /tmp/test-out-XXXXXX` test/build/perftools.c -lprofiler -L/home/MrThinh/grpc/libs/opt/protobuf -L/home/MrThinh/grpc/libs/opt/c-ares -g  -Llibs/opt -pthread   -L/home/MrThinh/grpc/libs/opt/zlib || true
test/build/perftools.c:19:33: fatal error: gperftools/profiler.h: No such file or directory
 #include <gperftools/profiler.h>
                                 ^
compilation terminated.
pkg-config --atleast-version=3.0.0 protobuf || true
protoc --version | grep -q libprotoc.3 || true
/bin/sh: protoc: command not found
pkg-config --atleast-version=1.11.0 libcares || true


MSYS2$ make



