cmake_minimum_required(VERSION 3.11)
project(RakNet)

if(WIN32)
	set(RAKNET_LIBRARY_LIBS ws2_32.lib)
else()
	set(RAKNET_LIBRARY_LIBS pthread)
endif()

file(GLOB RAKNET_HEADERS ${RakNet_SOURCE_DIR}/Source/*.h)
file(GLOB RAKNET_SOURCES ${RakNet_SOURCE_DIR}/Source/*.cpp)

add_library(RakNet SHARED ${RAKNET_SOURCES} ${RAKNET_HEADERS})

target_include_directories(RakNet PUBLIC ${RakNet_SOURCE_DIR}/Source)

target_link_libraries(RakNet ${RAKNET_LIBRARY_LIBS})

#IF(WIN32 AND NOT UNIX)
#	SET(CMAKE_CXX_FLAGS "/D WIN32 /D _RAKNET_DLL /D _CRT_NONSTDC_NO_DEPRECATE /D _CRT_SECURE_NO_DEPRECATE /GS- /GR- ")
#	target_link_libraries(RakNetDLL ${RAKNET_LIBRARY_LIBS})
#ELSE(WIN32 AND NOT UNIX)
#	target_link_libraries(RakNetDLL ${RAKNET_LIBRARY_LIBS})
#	INSTALL(TARGETS RakNetDLL DESTINATION ${RakNet_SOURCE_DIR}/Lib/DLL)
#ENDIF(WIN32 AND NOT UNIX)

if (WIN32)
	target_compile_definitions(RakNet PRIVATE _RAKNET_DLL)
endif ()

if(CMAKE_SIZEOF_VOID_P EQUAL 8)
	set_target_properties(RakNet PROPERTIES OUTPUT_NAME "RakNet64")
else()
	set_target_properties(RakNet PROPERTIES OUTPUT_NAME "RakNet32")
endif()