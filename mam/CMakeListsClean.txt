#[[
Copyright (c) 2018 IOTA Stiftung
https://github.com/iotaledger/entangled

Refer to the LICENSE file for licensing information
]]
set(ENTANGLED_DIR ${CMAKE_SOURCE_DIR})
set(UTILS_DIR ${CMAKE_SOURCE_DIR}/utils)
set(COMMON_DIR ${CMAKE_SOURCE_DIR}/common)
set(MAM_DIR ${CMAKE_SOURCE_DIR}/mam)

#add_definitions(COMPILE_DEFINITIONS   "MAM_MSS_TRAVERSAL")
#add_definitions(COMPILE_DEFINITIONS_<MAM_MSS_TRAVERSAL>)
#SET(COMPILE_DEFINITIONS_<MAM_MSS_TRAVERSAL>)


set(COMPONENT_PRIV_INCLUDEDIRS ${ENTANGLED_DIR})
# common/errors
set(COMMON_ERROR
    ${COMMON_DIR}/errors.c
)
# utils
set(UTILS
    ${UTILS_DIR}/time.c
    ${UTILS_DIR}/logger_helper.c
    ${UTILS_DIR}/handles/socket.c
    ${UTILS_DIR}/char_buffer.c
    ${UTILS_DIR}/memset_safe.c
)
# trinary
set(COMMON_TRINARY
    ${COMMON_DIR}/trinary/add.c
    ${COMMON_DIR}/trinary/flex_trit.c
    ${COMMON_DIR}/trinary/ptrit_incr.c
    ${COMMON_DIR}/trinary/trit_array.c
    ${COMMON_DIR}/trinary/trit_byte.c
    ${COMMON_DIR}/trinary/trit_long.c
    ${COMMON_DIR}/trinary/trit_ptrit.c
    ${COMMON_DIR}/trinary/trit_tryte.c
    ${COMMON_DIR}/trinary/tryte_ascii.c
    ${COMMON_DIR}/trinary/tryte_long.c
)
#http client
set(HTTP_CLIENT
    ${CCLIENT_DIR}/http/http.c
    ${CCLIENT_DIR}/service.c
)
#hash container
set(HASH_CONTAINERS
    ${HASH_CONTAINERS_DIR}/hash_array.c
    ${HASH_CONTAINERS_DIR}/hash27_queue.c
    ${HASH_CONTAINERS_DIR}/hash81_queue.c
    ${HASH_CONTAINERS_DIR}/hash243_queue.c
    ${HASH_CONTAINERS_DIR}/hash6561_queue.c
    ${HASH_CONTAINERS_DIR}/hash8019_queue.c
    ${HASH_CONTAINERS_DIR}/hash27_stack.c
    ${HASH_CONTAINERS_DIR}/hash81_stack.c
    ${HASH_CONTAINERS_DIR}/hash243_stack.c
    ${HASH_CONTAINERS_DIR}/hash6561_stack.c
    ${HASH_CONTAINERS_DIR}/hash8019_stack.c
)
# common curl
set(COMMON_CURL
    ${COMMON_DIR}/crypto/curl-p/const.c
    ${COMMON_DIR}/crypto/curl-p/curl_p.c
    ${COMMON_DIR}/crypto/curl-p/digest.c
)
set(COMMON_KERL
    ${COMMON_DIR}/crypto/kerl/bigint.c
    ${COMMON_DIR}/crypto/kerl/converter.c
    ${COMMON_DIR}/crypto/kerl/kerl.c
    ${COMMON_DIR}/crypto/kerl/hash.c
)
set(COMMON_HELPERS
    ${COMMON_DIR}/helpers/checksum.c
    ${COMMON_DIR}/helpers/digest.c
    ${COMMON_DIR}/helpers/sign.c
)
set(COMMON_MODEL
    ${COMMON_DIR}/model/bundle.c
    ${COMMON_DIR}/model/transaction.c
    ${COMMON_DIR}/model/transfer.c
)
set(COMMON_SIGN
    ${COMMON_DIR}/crypto/iss/v1/iss_curl.c
    ${COMMON_DIR}/crypto/iss/v1/iss_kerl.c
    ${COMMON_DIR}/crypto/iss/normalize.c
)

set(COMMON_CRYPTO
    ${COMMON_DIR}/crypto/ftroika/ftroika.c
    ${COMMON_DIR}/crypto/troika/troika.c
    ${COMMON_DIR}/crypto/ftroika/ftroika.h
    ${COMMON_DIR}/crypto/troika/troika.h
)

set(COMMON_SRC
    ${COMMON_ERROR}
    ${COMMON_TRINARY}
    ${COMMON_CURL}
    ${COMMON_KERL}
    ${COMMON_HELPERS}
    ${COMMON_MODEL}
    ${COMMON_SIGN}
    ${COMMON_CRYPTO}
)

add_library(libcommon
  ${COMMON_SRC}
)

add_dependencies(libcommon
  cclient
  #common
)

target_link_libraries(libcommon PUBLIC
  #cclient
  #common
  ${EXTERNAL_LINK_LIBS}
  ${EXT_LIB_UNITY}
  Threads::Threads
)


install(TARGETS libcommon DESTINATION "${CMAKE_INSTALL_PREFIX}/lib")
install(DIRECTORY "${PROJECT_SOURCE_DIR}/libcommon/" DESTINATION
"${CMAKE_INSTALL_PREFIX}/include/entangled/libcommon" FILES_MATCHING PATTERN "*.h")

#==============mam source=====================
# mam-api
set(MAM_API_DIR ${MAM_DIR}/api)
set(MAM_API
    ${MAM_API_DIR}/api.c
    ${MAM_API_DIR}/trit_t_to_mam_msg_read_context_t_map.c
    ${MAM_API_DIR}/trit_t_to_mam_msg_write_context_t_map.c
)

# mam-examples
set(MAM_EXAMPLES_DIR ${MAM_DIR}/examples)
set(MAM_EXAMPLES
    ${MAM_EXAMPLES_DIR}/common.c
    ${MAM_EXAMPLES_DIR}/recv.c
    ${MAM_EXAMPLES_DIR}/send-common.c
    ${MAM_EXAMPLES_DIR}/send-header.c
    ${MAM_EXAMPLES_DIR}/send-msg.c
    ${MAM_EXAMPLES_DIR}/send-packet.c
)

# mam-mam
set(MAM_MAM_DIR ${MAM_DIR}/mam)
set(MAM_MAM
    ${MAM_MAM_DIR}/channel.c
    ${MAM_MAM_DIR}/endpoint.c
    ${MAM_MAM_DIR}/message.c
    ${MAM_MAM_DIR}/mam_channel_t_set.c
    ${MAM_MAM_DIR}/mam_endpoint_t_set.c
    ${MAM_MAM_DIR}/mam_pk_t_set.c
)

# mam-mss
set(MAM_MSS_DIR ${MAM_DIR}/mss)
set(MAM_MSS
#    ${MAM_MSS_DIR}/mss_classic.c
    ${MAM_MSS_DIR}/mss_common.c
    ${MAM_MSS_DIR}/mss_traversal.c
    ${MAM_MSS_DIR}/mss.h
)

# mam-ntru
set(MAM_NTRU_DIR ${MAM_DIR}/ntru)
set(MAM_NTRU
    ${MAM_NTRU_DIR}/ntru.c
    ${MAM_NTRU_DIR}/poly.c
    ${MAM_NTRU_DIR}/mam_ntru_pk_t_set.c
    ${MAM_NTRU_DIR}/mam_ntru_sk_t_set.c
)

# mam-pb3
set(MAM_PB3_DIR ${MAM_DIR}/pb3)
set(MAM_PB3
    ${MAM_PB3_DIR}/pb3.c
)

# mam-prng
set(MAM_PRNG_DIR ${MAM_DIR}/prng)
set(MAM_PRNG
    ${MAM_PRNG_DIR}/prng.c
)

# mam-prototype
set(MAM_PROTOTYPE_DIR ${MAM_DIR}/prototype)
set(MAM_PROTOTYPE
    ${MAM_PROTOTYPE_DIR}/mam.c
    ${MAM_PROTOTYPE_DIR}/mask.c
)

# mam-psk
set(MAM_PSK_DIR ${MAM_DIR}/psk)
set(MAM_PSK
    ${MAM_PSK_DIR}/psk.c
    ${MAM_PSK_DIR}/mam_psk_t_set.c
)

# mam-sponge
set(MAM_SPONGE_DIR ${MAM_DIR}/sponge)
set(MAM_SPONGE
    ${MAM_SPONGE_DIR}/sponge.c
    ${MAM_SPONGE_DIR}/spongos_types.c
    ${MAM_SPONGE_DIR}/spongos.c
)

# mam-trits
set(MAM_TRITS_DIR ${MAM_DIR}/trits)
set(MAM_TRITS
    ${MAM_TRITS_DIR}/buffers.c
    ${MAM_TRITS_DIR}/trits.c
)

# mam-troika
set(MAM_TROIKA_DIR ${MAM_DIR}/troika)
set(MAM_TROIKA
    ${MAM_TROIKA_DIR}/troika.c
    ${MAM_TROIKA_DIR}/troika.h
)

# mam-wots
set(MAM_WOTS_DIR ${MAM_DIR}/wots)
set(MAM_WOTS
    ${MAM_WOTS_DIR}/wots.c
)

# mam
set(MAM
    ${MAM_API}
    ${MAM_EXAMPLES}
    ${MAM_MAM}
    ${MAM_MSS}
    ${MAM_NTRU}
    ${MAM_PB3}
    ${MAM_PRNG}
    ${MAM_PROTOTYPE}
    ${MAM_PSK}
    ${MAM_SPONGE}
    ${MAM_TRITS}
    ${MAM_TROIKA}
    ${MAM_WOTS}
)


#==============end of mam source=====================

## libmam
#add_library(mamLib
#  ${MAM}
#)

set(COMPONENT_ADD_INCLUDEDIRS ${CMAKE_CURRENT_LIST_DIR}/${ENTANGLED_DIR})
# local components
set(COMPONENT_REQUIRES
   embear_logger
   uthash
   http_parser
   keccak
   mbedtls
)

# esp-idf compoments
set(COMPONENT_PRIV_REQUIRES
    json
)


# flex_trit encoding
if(CONFIG_ONE_TRIT_PER_BYTE)
    add_definitions(-DFLEX_TRIT_ENCODING_1_TRITS_PER_BYTE)
elseif(CONFIG_THREE_TRIT_PER_BYTE)
    add_definitions(-DFLEX_TRIT_ENCODING_3_TRITS_PER_BYTE)
elseif(CONFIG_FOUR_TRIT_PER_BYTE)
    add_definitions(-DFLEX_TRIT_ENCODING_4_TRITS_PER_BYTE)
elseif(CONFIG_FIVE_TRIT_PER_BYTE)
    add_definitions(-DFLEX_TRIT_ENCODING_5_TRITS_PER_BYTE)
endif()

#include(ExternalProject)

#include(../cmake/embear_logger.cmake)
#include(../cmake/keccak.cmake)
#include(../cmake/mbedtls.cmake)
#include(../cmake/unity.cmake)
#include(../cmake/uthash.cmake)

link_directories("${CMAKE_INSTALL_PREFIX}/lib")



include_directories(
  "${CMAKE_INSTALL_PREFIX}/include"
  "${PROJECT_SOURCE_DIR}"
)

add_library(libmam ${MAM})
target_link_libraries(libmam PUBLIC cclient libcommon)

install(TARGETS libmam DESTINATION "${CMAKE_INSTALL_PREFIX}/lib")
install(DIRECTORY "${PROJECT_SOURCE_DIR}/libmam/" DESTINATION
"${CMAKE_INSTALL_PREFIX}/include/entangled/libmam" FILES_MATCHING PATTERN "*.h")


add_executable(send-msg examples/send-msg.c)
#target_include_directories(send-msg PUBLIC
#"${CMAKE_INSTALL_PREFIX}/lib"
#"${CMAKE_INSTALL_PREFIX}/include/entangled/common"
#"${CMAKE_INSTALL_PREFIX}/include/entangled/utils"
#"${PROJECT_BINARY_DIR}/external"
#"${PROJECT_BINARY_DIR}/download"
#"${PROJECT_BINARY_DIR}/install"
#"${PROJECT_BINARY_DIR}/install/bin"
#"${EXTERNAL_INSTALL_DIR}/include"
#${COMMON_SRC}
#)



target_link_libraries(send-msg PUBLIC
  #common
  libcommon
  #cclient
  libmam
)
