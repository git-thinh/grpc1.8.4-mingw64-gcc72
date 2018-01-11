msys2 (with mingw)

The Makefile (and source code) should support msys2's mingw32 and mingw64 compilers. Building with msys2's native compiler is also possible, but difficult.

This approach requires having msys2 installed.

# Install prerequisites

MSYS2$ pacman -S autoconf automake gcc libtool mingw-w64-x86_64-toolchain perl pkg-config zlib
MSYS2$ pacman -S mingw-w64-x86_64-gflags

# From mingw shell

MINGW64$ export CPPFLAGS="-D_WIN32_WINNT=0x0600"
MINGW64$ make

NOTE: While most of the make targets are buildable under Mingw, some haven't been ported to Windows yet and may fail to build (mostly trying to include POSIX headers not available on Mingw).