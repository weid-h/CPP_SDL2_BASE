# CPPSDL2BASE

Base c++ project with SDL2

## Instructions for windows:

- Edit CMakeLists row 11 include the path to SDL2.
- You may also need to edit rows 35-37 to copy the DLL to the output folder correctly
- Run cmake with the correct build configuration in your build directory `cmake -DCMAKE_BUILD_TYPE:STRING=Debug -G "MinGW Makefiles" ..`
