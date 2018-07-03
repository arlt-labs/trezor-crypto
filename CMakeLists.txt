cmake_minimum_required(VERSION 3.10)

# project name and version should be set after cmake_policy CMP0048
project(trezor-crypt)

set(SOURCE_FILES
        address.c
        address.h
        base32.c
        base32.h
        base58.c
        base58.h
        bignum.c
        bignum.h
        bip32.c
        bip32.h
        bip39.c
        bip39.h
        bip39_english.h
        blake256.c
        blake256.h
        blake2_common.h
        blake2b.c
        blake2b.h
        blake2s.c
        blake2s.h
        cash_addr.c
        cash_addr.h
        check_mem.h
        curves.c
        curves.h
        ecdsa.c
        ecdsa.h
        groestl.c
        groestl.h
        groestl_internal.h
        hasher.c
        hasher.h
        hmac.c
        hmac.h
        memzero.c
        memzero.h
        nem.c
        nem.h
        nem_serialize.h
        nist256p1.c
        nist256p1.h
        options.h
        pbkdf2.c
        pbkdf2.h
        rand.c
        rand.h
        rc4.c
        rc4.h
        rfc6979.c
        rfc6979.h
        ripemd160.c
        ripemd160.h
        script.c
        script.h
        secp256k1.c
        secp256k1.h
        segwit_addr.c
        segwit_addr.h
        sha2.c
        sha2.h
        sha3.c
        sha3.h

        aes/aes.h
        aes/aes_modes.c
        aes/aescrypt.c
        aes/aeskey.c
        aes/aesopt.h
        aes/aestab.c
        aes/aestab.h
        aes/aestst.c
        aes/aestst.h
        aes/brg_types.h

        chacha20poly1305/chacha20poly1305.c
        chacha20poly1305/chacha20poly1305.h
        chacha20poly1305/chacha_merged.c
        chacha20poly1305/ecrypt-config.h
        chacha20poly1305/ecrypt-machine.h
        chacha20poly1305/ecrypt-portable.h
        chacha20poly1305/ecrypt-sync.h
        chacha20poly1305/poly1305-donna-32.h
        chacha20poly1305/poly1305-donna.c
        chacha20poly1305/poly1305-donna.h
        chacha20poly1305/rfc7539.c
        chacha20poly1305/rfc7539.h

        ed25519-donna/curve25519-donna-32bit.c
        ed25519-donna/curve25519-donna-32bit.h
        ed25519-donna/curve25519-donna-helpers.c
        ed25519-donna/curve25519-donna-helpers.h
        ed25519-donna/curve25519-donna-scalarmult-base.c
        ed25519-donna/curve25519-donna-scalarmult-base.h
        ed25519-donna/ed25519-donna-32bit-tables.c
        ed25519-donna/ed25519-donna-32bit-tables.h
        ed25519-donna/ed25519-donna-basepoint-table.c
        ed25519-donna/ed25519-donna-basepoint-table.h
        ed25519-donna/ed25519-donna-impl-base.c
        ed25519-donna/ed25519-donna-impl-base.h
        ed25519-donna/ed25519-donna-portable.h
        ed25519-donna/ed25519-donna.h
        ed25519-donna/ed25519-hash-custom-keccak.h
        ed25519-donna/ed25519-hash-custom-sha3.h
        ed25519-donna/ed25519-hash-custom.h
        ed25519-donna/ed25519-keccak.c
        ed25519-donna/ed25519-keccak.h
        ed25519-donna/ed25519-sha3.c
        ed25519-donna/ed25519-sha3.h
        ed25519-donna/ed25519.c
        ed25519-donna/ed25519.h
        ed25519-donna/modm-donna-32bit.c
        ed25519-donna/modm-donna-32bit.h
        )

add_library(trezor-crypto ${SOURCE_FILES})

set_property(TARGET trezor-crypto PROPERTY C_STANDARD 99)
target_include_directories(trezor-crypto SYSTEM PRIVATE ${CMAKE_CURRENT_SOURCE_DIR})
target_compile_definitions(trezor-crypto PRIVATE USE_ETHEREUM=1 USE_GRAPHENE=1 USE_NEM=1 USE_MONERO=1 RAND_PLATFORM_INDEPENDENT=1)
install(DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR} DESTINATION include
    FILES_MATCHING PATTERN "*.h"
    PATTERN "tests/*" EXCLUDE
    PATTERN "gui/*" EXCLUDE
    PATTERN ".git/*" EXCLUDE)
install(TARGETS trezor-crypto ARCHIVE DESTINATION lib)

