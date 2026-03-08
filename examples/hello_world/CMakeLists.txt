file(GLOB SOURCES 
	*.cpp
	MainFrame/*.cpp)

include_directories(.)

add_executable(hello_world ${SOURCES})

target_link_libraries(hello_world wui)
