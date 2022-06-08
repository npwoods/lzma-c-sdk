cmake_minimum_required (VERSION 3.15)
project (lzma C)

include(GNUInstallDirs)

set(CMAKE_DEBUG_POSTFIX "d")

set(LZMA_SOURCES
	src/7zAlloc.c
	src/7zArcIn.c
	src/7zBuf.c
	src/7zBuf2.c
	src/7zCrc.c
	src/7zCrcOpt.c
	src/7zDec.c
	src/7zFile.c
	src/7zStream.c
	src/Aes.c
	src/AesOpt.c
	src/Alloc.c
	src/Bcj2.c
	src/Bcj2Enc.c
	src/Bra.c
	src/Bra86.c
	src/BraIA64.c
	src/CpuArch.c
	src/Delta.c
	src/DllSecur.c
	src/LzFind.c
	src/LzFindMt.c
	src/Lzma2Dec.c
	src/Lzma2DecMt.c
	src/Lzma2Enc.c
	src/Lzma86Dec.c
	src/Lzma86Enc.c
	src/LzmaDec.c
	src/LzmaEnc.c
	src/LzmaLib.c
	src/MtCoder.c
	src/MtDec.c
	src/Ppmd7.c
	src/Ppmd7Dec.c
	src/Ppmd7Enc.c
	src/Sha256.c
	src/Sort.c
	src/Threads.c
	src/Xz.c
	src/XzCrc64.c
	src/XzCrc64Opt.c
	src/XzDec.c
	src/XzEnc.c
	src/XzIn.c)

set(LZMA_HEADERS
	src/7z.h
	src/7zAlloc.h
	src/7zBuf.h
	src/7zCrc.h
	src/7zFile.h
	src/7zTypes.h
	src/7zVersion.h
	src/Aes.h
	src/Alloc.h
	src/Bcj2.h
	src/Bra.h
	src/Compiler.h
	src/CpuArch.h
	src/Delta.h
	src/DllSecur.h
	src/LzFind.h
	src/LzFindMt.h
	src/LzHash.h
	src/Lzma2Dec.h
	src/Lzma2DecMt.h
	src/Lzma2Enc.h
	src/Lzma86.h
	src/LzmaDec.h
	src/LzmaEnc.h
	src/LzmaLib.h
	src/MtCoder.h
	src/MtDec.h
	src/Ppmd.h
	src/Ppmd7.h
	src/Precomp.h
	src/RotateDefs.h
	src/Sha256.h
	src/Sort.h
	src/Threads.h
	src/Xz.h
	src/XzCrc64.h
	src/XzEnc.h)

add_library(${PROJECT_NAME} ${LZMA_SOURCES} ${LZMA_HEADERS})

set_target_properties(${PROJECT_NAME} PROPERTIES
	LINKER_LANGUAGE C
	PUBLIC_HEADER "${LZMA_HEADERS}")

# configure the LZMAConfig.cmake file
set(CONF_LIBRARIES ${PROJECT_NAME}d)
configure_file(LZMAConfig.cmake.in "${CMAKE_CURRENT_BINARY_DIR}${CMAKE_FILES_DIRECTORY}/LZMAConfig.dbg.cmake" @ONLY)
set(CONF_LIBRARIES ${PROJECT_NAME})
configure_file(LZMAConfig.cmake.in "${CMAKE_CURRENT_BINARY_DIR}${CMAKE_FILES_DIRECTORY}/LZMAConfig.rel.cmake" @ONLY)

install(
    TARGETS ${PROJECT_NAME}
    LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR}d
    PUBLIC_HEADER DESTINATION "${CMAKE_INSTALL_INCLUDEDIR}/lzma"
)

install(FILES "${CMAKE_CURRENT_BINARY_DIR}${CMAKE_FILES_DIRECTORY}/LZMAConfig.dbg.cmake" RENAME LZMAConfig.cmake CONFIGURATIONS Debug DESTINATION lib/cmake/lzma)
install(FILES "${CMAKE_CURRENT_BINARY_DIR}${CMAKE_FILES_DIRECTORY}/LZMAConfig.rel.cmake" RENAME LZMAConfig.cmake CONFIGURATIONS Release DESTINATION lib/cmake/lzma)
