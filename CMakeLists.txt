cmake_minimum_required(VERSION 3.11)
project(RakNet)

if(WIN32)
	set(RAKNET_LIBRARY_LIBS ws2_32.lib)
else()
	set(RAKNET_LIBRARY_LIBS pthread)
endif()

file(GLOB RAKNET_HEADERS ${RakNet_SOURCE_DIR}/Source/*.h)
file(GLOB RAKNET_SOURCES ${RakNet_SOURCE_DIR}/Source/*.cpp)

add_library(RakNet STATIC ${RAKNET_SOURCES} ${RAKNET_HEADERS})

target_include_directories(RakNet PUBLIC ${RakNet_SOURCE_DIR}/Source)

target_link_libraries(RakNet ${RAKNET_LIBRARY_LIBS})