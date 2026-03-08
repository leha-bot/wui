file(GLOB SOURCES 
	*.cpp)

include_directories(.)

add_executable(simple ${SOURCES})

target_link_libraries(simple wui)
