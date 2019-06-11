# # ficapi��
# The Shrug License

# Copyright � 2018 ThePhD. All rights can sometimes maybe not unreserved, yo.

set(ficapi_sources
	"include/ficapi/ficapi.hpp"
	"include/ficapi/c_api.hpp"
	"include/ficapi/c++_api.hpp"
	"source/c_api.cpp"
	"source/c++_api.cpp"
)

add_library(ficapi SHARED ${ficapi_sources})
set_target_properties(ficapi PROPERTIES
	CXX_STANDARD 11
	CXX_STANDARD_REQUIRED ON
	CXX_EXTENSIONS OFF)
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


