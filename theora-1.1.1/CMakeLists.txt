cmake_minimum_required(VERSION 2.8)

set(THEORA_DEC_SRC
    lib/apiwrapper.c
    lib/bitpack.c
    lib/decapiwrapper.c
    lib/decinfo.c
    lib/decode.c
    lib/dequant.c
    lib/fragment.c
    lib/huffdec.c
    lib/idct.c
    lib/info.c
    lib/internal.c
    lib/quant.c
    lib/state.c)

if( "${ARCH}" STREQUAL "x86_64" )
    list(APPEND THEORA_DEC_SRC
        lib/x86/mmxidct.c
        lib/x86/mmxfrag.c
        lib/x86/mmxstate.c
        lib/x86/x86state.c)
endif( "${ARCH}" STREQUAL "x86_64" )

add_library(theoradec ${THEORA_DEC_SRC})

set(THEORA_HEADERS include/theora/codec.h include/theora/theora.h include/theora/theoradec.h)

include_directories("./include")

# For ogg headers
include_directories("${PROJECT_SOURCE_DIR}/ogg-1.3.2/include")

# For ogg configured headers
include_directories("${PROJECT_BINARY_DIR}/ogg-1.3.2/include")

install(FILES ${THEORA_HEADERS} DESTINATION include/theora)
