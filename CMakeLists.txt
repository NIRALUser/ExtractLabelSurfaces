Project(ExtractLabelSurfaceSuperBuild)
cmake_minimum_required(VERSION 2.8.11)

include(${CMAKE_CURRENT_SOURCE_DIR}/Common.cmake)

option( ExtractLabelSurface_SuperBuild
        "Build ExtractLabelSurface as a Superbuild project" ON )
if( ExtractLabelSurface_SuperBuild )
  include("${CMAKE_CURRENT_SOURCE_DIR}/SuperBuild.cmake")
else()
  include("${CMAKE_CURRENT_SOURCE_DIR}/ExtractLabelSurfaces.cmake")
endif()


