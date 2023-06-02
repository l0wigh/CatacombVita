cmake_minimum_required(VERSION 3.19)

if(NOT DEFINED CMAKE_TOOLCHAIN_FILE)
  if(DEFINED ENV{VITASDK})
    set(CMAKE_TOOLCHAIN_FILE "$ENV{VITASDK}/share/vita.toolchain.cmake" CACHE PATH "toolchain file")
  else()
    message(FATAL_ERROR "Please define VITASDK to point to your SDK path!")
  endif()
endif()

project(Catacomb-Vita)

include("$ENV{VITASDK}/share/vita.cmake" REQUIRED)

set(SRC ${CMAKE_CURRENT_SOURCE_DIR})
set(BIN ${CMAKE_CURRENT_BINARY_DIR})

set(VITA_APP_NAME "Catacomb")

set(VITA_TITLEID  "CTCB00000")

set(VITA_VERSION  "01.00")

set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -Wall -g -O0")
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -g -O0 -std=c++11")

set(VITA_MKSFOEX_FLAGS "${VITA_MKSFOEX_FLAGS} -d PARENTAL_LEVEL=1 -d ATTRIBUTE2=12")



include_directories()


link_directories(
  ${CMAKE_CURRENT_BINARY_DIR}
)

# Add all the files needed to compile here
add_executable(${PROJECT_NAME}
 	srcs/cat_play.c
 	srcs/catacomb.c
 	srcs/catasm.c
 	srcs/cpanel.c
 	srcs/objects.c
 	srcs/pcrlib_a.c
 	srcs/pcrlib_c.c
 	srcs/rleasm.c
)

# Library to link to (drop the -l prefix). This will mostly be stubs.
target_link_libraries(${PROJECT_NAME}
	SDL2
	SDL2_image
	SDL2_mixer
	SceDisplay_stub
	SceCtrl_stub
	SceAudio_stub
	SceAudioIn_stub
	SceSysmodule_stub
	SceGxm_stub
	SceCommonDialog_stub
	SceAppMgr_stub
	SceTouch_stub
	SceHid_stub
	SceMotion_stub
	m
	z
	physfs
	jpeg
	png
	webp
	mikmod
	mpg123
	vorbis
	vorbisfile
	ogg
	pthread
	FLAC
)

target_include_directories(${PROJECT_NAME} PRIVATE
   "${VITASDK}/arm-vita-eabi/include/SDL2"
)

# file( GLOB_RECURSE RES RELATIVE ${CMAKE_CURRENT_SOURCE_DIR} res/*)
# file( GLOB_RECURSE CONFIG RELATIVE ${CMAKE_CURRENT_SOURCE_DIR} config/*)
#
# set(RESDATA "")
#
# FOREACH(ITEM ${RES})
#   list(APPEND RESDATA "FILE")
#   list(APPEND RESDATA ${ITEM})
#   list(APPEND RESDATA ${ITEM})
# ENDFOREACH()
#
# set(CONFIGDATA "")
#
# FOREACH(ITEM ${CONFIG})
#   list(APPEND CONFIGDATA "FILE")
#   list(APPEND CONFIGDATA ${ITEM})
#   list(APPEND CONFIGDATA ${ITEM})
# ENDFOREACH()

## Create Vita files
vita_create_self(${PROJECT_NAME}.self ${PROJECT_NAME} UNSAFE)
vita_create_vpk(${PROJECT_NAME}.vpk ${VITA_TITLEID} ${PROJECT_NAME}.self
  VERSION ${VITA_VERSION}
  NAME ${VITA_APP_NAME}

	# ${CONFIGDATA}
	# ${RESDATA}
  
    # livearea + boot
	FILE sce_sys/icon0.png sce_sys/icon0.png
	FILE sce_sys/pic0.png sce_sys/pic0.png
	FILE sce_sys/livearea/contents/bg0.png sce_sys/livearea/contents/bg0.png
	FILE sce_sys/livearea/contents/template.xml sce_sys/livearea/contents/template.xml
)
