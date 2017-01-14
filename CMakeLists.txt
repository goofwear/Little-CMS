cmake_minimum_required(VERSION 3.2)

project(lcms2 VERSION 2.8 LANGUAGES C)

if(MSVC)
  set(CMAKE_DEBUG_POSTFIX "d")
endif()

add_library(lcms2
  ${CMAKE_CURRENT_SOURCE_DIR}/src/cmsnamed.c
  ${CMAKE_CURRENT_SOURCE_DIR}/src/cmsopt.c
  ${CMAKE_CURRENT_SOURCE_DIR}/src/cmspack.c
  ${CMAKE_CURRENT_SOURCE_DIR}/src/cmspcs.c
  ${CMAKE_CURRENT_SOURCE_DIR}/src/cmsplugin.c
  ${CMAKE_CURRENT_SOURCE_DIR}/src/cmsps2.c
  ${CMAKE_CURRENT_SOURCE_DIR}/src/cmssamp.c
  ${CMAKE_CURRENT_SOURCE_DIR}/src/cmssm.c
  ${CMAKE_CURRENT_SOURCE_DIR}/src/cmstypes.c
  ${CMAKE_CURRENT_SOURCE_DIR}/src/cmsvirt.c
  ${CMAKE_CURRENT_SOURCE_DIR}/src/cmswtpnt.c
  ${CMAKE_CURRENT_SOURCE_DIR}/src/cmsxform.c
  ${CMAKE_CURRENT_SOURCE_DIR}/src/lcms2.def
  ${CMAKE_CURRENT_SOURCE_DIR}/src/lcms2_internal.h
  ${CMAKE_CURRENT_SOURCE_DIR}/src/cmsalpha.c
  ${CMAKE_CURRENT_SOURCE_DIR}/src/cmscam02.c
  ${CMAKE_CURRENT_SOURCE_DIR}/src/cmscgats.c
  ${CMAKE_CURRENT_SOURCE_DIR}/src/cmscnvrt.c
  ${CMAKE_CURRENT_SOURCE_DIR}/src/cmserr.c
  ${CMAKE_CURRENT_SOURCE_DIR}/src/cmsgamma.c
  ${CMAKE_CURRENT_SOURCE_DIR}/src/cmsgmt.c
  ${CMAKE_CURRENT_SOURCE_DIR}/src/cmshalf.c
  ${CMAKE_CURRENT_SOURCE_DIR}/src/cmsintrp.c
  ${CMAKE_CURRENT_SOURCE_DIR}/src/cmsio0.c
  ${CMAKE_CURRENT_SOURCE_DIR}/src/cmsio1.c
  ${CMAKE_CURRENT_SOURCE_DIR}/src/cmslut.c
  ${CMAKE_CURRENT_SOURCE_DIR}/src/cmsmd5.c
  ${CMAKE_CURRENT_SOURCE_DIR}/src/cmsmtrx.c
  ${CMAKE_CURRENT_SOURCE_DIR}/include/lcms2.h
  ${CMAKE_CURRENT_SOURCE_DIR}/include/lcms2_plugin.h
)

target_include_directories(lcms2
  PRIVATE
  $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/src;${CMAKE_CURRENT_SOURCE_DIR}/include;>
  INTERFACE
  $<INSTALL_INTERFACE:include>
  PUBLIC
  $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include>
)

target_compile_definitions(lcms2
  PRIVATE
  _CRT_SECURE_NO_WARNINGS
  _CRT_STDC_NO_DEPRECATE
)

include(CMakePackageConfigHelpers)
write_basic_package_version_file(
  ${CMAKE_CURRENT_BINARY_DIR}/${PROJECT_NAME}-config-version.cmake
  VERSION ${PROJECT_VERSION}
  COMPATIBILITY AnyNewerVersion
)

install(TARGETS lcms2 EXPORT lcms2
  RUNTIME DESTINATION bin
  ARCHIVE DESTINATION lib
  LIBRARY DESTINATION lib
)

install(FILES
  ${CMAKE_CURRENT_SOURCE_DIR}/include/lcms2.h
  ${CMAKE_CURRENT_SOURCE_DIR}/include/lcms2_plugin.h
  DESTINATION include
)

install(EXPORT lcms2
  FILE
  ${PROJECT_NAME}.cmake
  NAMESPACE
    lcms2::
  DESTINATION
    lib/cmake/${PROJECT_NAME}
)

install(FILES
  cmake/${PROJECT_NAME}-config.cmake
  ${CMAKE_CURRENT_BINARY_DIR}/${PROJECT_NAME}-config-version.cmake
  DESTINATION
    lib/cmake/${PROJECT_VERSION}
)

export(TARGETS ${PROJECT_NAME}
  FILE
  ${CMAKE_CURRENT_BINARY_DIR}/${PROJECT_NAME}-config.cmake
  NAMESPACE ${PROJECT_NAME}::
)