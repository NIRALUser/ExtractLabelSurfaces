Project(ExtractLabelSurfaceSuperBuild)
cmake_minimum_required(VERSION 2.8.11)

set(CMAKE_MODULE_PATH
	${${PROJECT_NAME}_SOURCE_DIR}/CMake
	${${PROJECT_NAME}_BINARY_DIR}/CMake
	${CMAKE_MODULE_PATH}
)

include(${CMAKE_CURRENT_SOURCE_DIR}/Common.cmake)

option( ExtractLabelSurface_SuperBuild
        "Build ExtractLabelSurface as a Superbuild project" ON )
if( ExtractLabelSurface_SuperBuild )
  include("${CMAKE_CURRENT_SOURCE_DIR}/SuperBuild.cmake")
else()
  include("${CMAKE_CURRENT_SOURCE_DIR}/ExtractLabelSurfaces.cmake")
endif()


