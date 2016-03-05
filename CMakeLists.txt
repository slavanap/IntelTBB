project(IntelTBB)

if(WIN32 OR MINGW OR CYGWIN)
	if (CMAKE_SIZEOF_VOID_P EQUAL 4)
		set(libpath "lib/ia32/vc10/tbb.lib")
	elseif(CMAKE_SIZEOF_VOID_P EQUAL 8)
		set(libpath "lib/intel64/vc10/tbb.lib")
	else()
		error("Unknown sizeof(void*) value ${CMAKE_SIZEOF_VOID_P}")
	endif()
elseif(UNIX)
	if (CMAKE_SIZEOF_VOID_P EQUAL 4)
		set(libpath "lib/ia32/gcc4.4/libtbb.so.2")
	elseif(CMAKE_SIZEOF_VOID_P EQUAL 8)
		set(libpath "lib/intel64/gcc4.4/libtbb.so.2")
	else()
		error("Unknown sizeof(void*) value ${CMAKE_SIZEOF_VOID_P}")
	endif()
endif()

add_library(${PROJECT_NAME} STATIC IMPORTED GLOBAL)
set_target_properties(${PROJECT_NAME} PROPERTIES
	IMPORTED_LOCATION "${CMAKE_CURRENT_LIST_DIR}/${libpath}"
	LINKER_LANGUAGE CXX
	FOLDER "Third Party"
)
set(INTELTBB_INCLUDE_DIR "${CMAKE_CURRENT_LIST_DIR}/include/tbb" PARENT_SCOPE)
