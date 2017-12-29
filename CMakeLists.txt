cmake_minimum_required(VERSION 2.8.9)
project(RPG_MODDING_API)

set(CMAKE_CXX_STANDARD 11)

include_directories(include)
include_directories(external_include)

include_directories(F:/Projects/C++/C++_LIBS/SFML-2.4.2/include)

if(WIN32)
	link_directories(link_win32)
endif(WIN32)

file(GLOB SOURCES "src/*.cpp" "include/*.h")

set(CMAKE_RUNTIME_OUTPUT_DIRECTORY bin)

add_library(RPG_MODDING_API SHARED ${SOURCES})

if(WIN32)
	target_link_libraries(RPG_MODDING_API sfml-window-2 sfml-graphics-2 sfml-system-2)
	add_custom_command(TARGET RPG_MODDING_API POST_BUILD COMMAND powershell cp bin/libRPG_MODDING_API.dll ../../../SFML_RPG/run/libRPG_MODDING_API.dll)
	add_custom_command(TARGET RPG_MODDING_API POST_BUILD COMMAND powershell cp bin/libRPG_MODDING_API.dll ../../../SFML_RPG/link/libRPG_MODDING_API.dll)
	add_custom_command(TARGET RPG_MODDING_API POST_BUILD COMMAND powershell cp bin/libRPG_MODDING_API.dll ../../../RPG_TEST_MOD/link/libRPG_MODDING_API.dll)
elseif(UNIX)
	target_link_libraries(RPG_MODDING_API sfml-window sfml-graphics sfml-system)
add_custom_command(TARGET RPG_MODDING_API POST_BUILD COMMAND cp bin/libRPG_MODDING_API.dll ../../../SFML_RPG/run/libRPG_MODDING_API.dll)
	add_custom_command(TARGET RPG_MODDING_API POST_BUILD COMMAND cp bin/libRPG_MODDING_API.dll ../../../SFML_RPG/link/libRPG_MODDING_API.dll)
	add_custom_command(TARGET RPG_MODDING_API POST_BUILD COMMAND cp bin/libRPG_MODDING_API.dll ../../../RPG_TEST_MOD/link/libRPG_MODDING_API.dll)
endif(WIN32)