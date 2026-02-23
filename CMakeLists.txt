cmake_minimum_required (VERSION 3.10)

project (wui LANGUAGES CXX C)

set(CMAKE_BUILD_TYPE Release)
set(CMAKE_CXX_STANDARD 17)

option(wui_USE_STATIC_STDLIB "Use static C++ stdlib (GCC/libstdc++ only)" OFF)

if(wui_USE_STATIC_STDLIB)
	set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -static-libstdc++ -static-libgcc")
endif()

set(CMAKE_MAKE_PROGRAM "make -j 3")

#set(CMAKE_CXX_FLAGS:STRING= -fsanitize=address  -fsanitize=leak -g)
#set(CMAKE_C_FLAGS:STRING=-fsanitize=address  -fsanitize=leak -g)
#set(CMAKE_EXE_LINKER_FLAGS:STRING=-fsanitize=address  -fsanitize=leak)
#set(CMAKE_MODULE_LINKER_FLAGS:STRING=-fsanitize=address  -fsanitize=leak)

include_directories(
	include)

link_directories(
	src)

add_subdirectory (src)
add_subdirectory (examples/hello_world)
add_subdirectory (examples/simple)
add_subdirectory (examples/demo)
