file(GLOB SOURCES 
    common/*.cpp
	control/*.cpp
	config/*.cpp
	event/*.cpp
	framework/*.cpp
	graphic/*.cpp
	theme/*.cpp
	theme/impl/*.cpp
	locale/*.cpp
	locale/impl/*.cpp
	system/*.cpp
	window/*.cpp)

find_package(PkgConfig REQUIRED)

pkg_check_modules(cairo REQUIRED IMPORTED_TARGET cairo)
# libudev-zero is a drop-in lib for some distros
pkg_check_modules(udev IMPORTED_TARGET libudev udev libudev-zero)

include_directories(. ../thirdparty)

add_library(wui STATIC ${SOURCES})
if(udev_FOUND)
    target_compile_definitions(wui PRIVATE HAVE_LIBUDEV=1)
    target_link_libraries(wui PUBLIC PkgConfig::udev)
endif()
target_link_libraries(wui PUBLIC PkgConfig::cairo)

