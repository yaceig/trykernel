cmake_minimum_required(VERSION 3.12)

set(CMAKE_TOOLCHAIN_FILE ../arm_toolchain.cmake)

# プロジェクトの基本設定
project(try-kernel C CXX ASM)
set(CMAKE_C_STANDARD 11)   # C言語の規格=C11
set(CMAKE_CXX_STANDARD 17) # C++言語の規格=C++17

# ソースコードの追加
add_executable(try-kernel
    application/main.c
    boot/boot2.c
    boot/reset_hdr.c
    boot/vector_tbl.c
    include/knldef.h
    include/sysdef.h
    include/syslib.h
    include/typedef.h
    linker/pico_memmap.ld
)

# Add include directory
target_include_directories(try-kernel PRIVATE include)
target_link_options(try-kernel PRIVATE -T ${CMAKE_SOURCE_DIR}/linker/pico_memmap.ld)
set_target_properties(${TARGET_NAME} PROPERTIES LINK_DEPENDS linker/pico_memmap.ld)
