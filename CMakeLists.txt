set(CMAKE_EXE_LINKER_FLAGS "${CMAKE_EXE_LINKER_FLAGS} -fuse-ld=lld")

cmake_minimum_required(VERSION 3.17)
project(convenienceFunctionForSoci VERSION 1.0.0
  DESCRIPTION convenienceFunctionForSoci
  LANGUAGES CXX
  ) 
cmake_policy(SET CMP0015 NEW)

####### create executable
set(TARGET_NAME imgui)

add_library(${TARGET_NAME}
"imconfig.h"
"imgui_demo.cpp"
"imgui_draw.cpp"
"imgui_internal.h"
"imgui_tables.cpp"
"imgui_widgets.cpp"
"imgui.cpp"
"imgui.h"
"imstb_rectpack.h"
"imstb_textedit.h"
"imstb_truetype.h"
)
add_subdirectory(misc)

set_target_properties(${TARGET_NAME} PROPERTIES LINKER_LANGUAGE CXX)
####### link
target_include_directories(${TARGET_NAME} PRIVATE ${CMAKE_CURRENT_BINARY_DIR})
target_include_directories(${TARGET_NAME} PRIVATE
  $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}>
  $<INSTALL_INTERFACE:${CMAKE_INSTALL_INCLUDEDIR}>
  )
  

target_link_libraries(${TARGET_NAME} PRIVATE ${PROJECT_WARNINGS} ${PROJECT_OPTIONS}

)

#print all variables used in cmake
# get_cmake_property(_variableNames VARIABLES)
# list (SORT _variableNames)
# foreach (_variableName ${_variableNames})
#    message(STATUS "${_variableName}=${${_variableName}}")
# endforeach()
