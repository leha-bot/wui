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


add_library(wui STATIC ${SOURCES})

# external thirdparty
if(wui_USE_BUNDLED_LIBS)
    include_directories(. ../thirdparty)
else()
    # boost nowide
    find_package(Boost REQUIRED COMPONENTS headers)
    find_package(nlohmann_json REQUIRED)
    find_package(utf8cpp REQUIRED)
    target_link_libraries(wui PUBLIC
	Boost::headers
	nlohmann_json::nlohmann_json
	utf8cpp::utf8cpp)
endif()

# system deps
if(udev_FOUND)
    target_compile_definitions(wui PRIVATE HAVE_LIBUDEV=1)
    target_link_libraries(wui PUBLIC PkgConfig::udev)
endif()
target_link_libraries(wui PUBLIC PkgConfig::cairo)

