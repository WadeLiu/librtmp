cmake_minimum_required(VERSION 3.5)

project(librtmp C)

add_definitions(
    -DUSE_OPENSSL
    -D_CRT_SECURE_NO_WARNINGS
)

set(SRCS
    rtmp.c
    log.c
    amf.c
    hashswf.c
    parseurl.c
    amf.h
    bytes.h
    dh.h
    dhgroups.h
    handshake.h
    http.h
    log.h
    rtmp_sys.h
    rtmp.h
)

FIND_PACKAGE(OpenSSL REQUIRED)
FIND_PACKAGE(ZLIB REQUIRED)

include_directories(
    ${CMAKE_SOURCE_DIR}
    ${OPENSSL_INCLUDE_DIR}
    ${ZLIB_INCLUDE_DIR}
)

add_library(librtmp STATIC
        ${SRCS}
)

target_link_libraries(librtmp PUBLIC ${OPENSSL_LIBRARIES} ${ZLIB_LIBRARIES})
