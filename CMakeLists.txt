# Copyright Ⓒ 2018-2019 ThePhD
# Distributed under the Boost Software License, Version 1.0.
# See accompanying file LICENSE_1_0.txt or copy at http://www.boost.org/LICENSE_1_0.txt

# Partial (add_subdirectory only) and experimental CMake support
# Subject to change; please do not rely on the contents of this file yet

set(ficapi_sources
	"include/ficapi/ficapi.hpp"
	"include/ficapi/c_api.hpp"
	"include/ficapi/c++_api.hpp"
	"source/c_api.cpp"
	"source/c++_api.cpp"
)

prepend(prefixed_ficapi_sources "${CMAKE_CURRENT_SOURCE_DIR}/" ${ficapi_sources})

add_library(ficapi SHARED ${prefixed_ficapi_sources})
if (MSVC)
	target_compile_options(ficapi
		PRIVATE /std:c++latest)
else()
	target_compile_options(ficapi
		PRIVATE -std=c++1z)
endif()
set_target_properties(ficapi
	PROPERTIES 
	POSITION_INDEPENDENT_CODE TRUE)
target_compile_definitions(ficapi
	PRIVATE FICAPI_BUILD=1
	PUBLIC FICAPI_DLL=1)
target_include_directories(ficapi
	PUBLIC "include")
target_link_libraries(ficapi 
	PUBLIC ${CMAKE_DL_LIBS})


