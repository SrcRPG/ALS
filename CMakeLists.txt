cmake_minimum_required(VERSION 3.14)
project(Als C CXX)
set(CMAKE_CXX_STANDARD 17)

add_subdirectory(libs/glfw)

if(APPLE)
    list(APPEND EXTRA_LIBS 
        "-framwork OpenGL"
        )
elseif(WIN32)
    list(APPEND EXTRA_LIBS 
        "-lglu32 -lopengl32"
        )
    set(CMAKE_EXE_LINKER_FLAGS "-std=gnu99 -static -static-libgcc -static-libstdc++ -mwindows")
else()
    list(APPEND EXTRA_LIBS
        "-lGL  -lX11"
        )
endif()

add_executable(Als src/main.cpp)
target_link_libraries(Als glfw ${EXTRA_LIBS})