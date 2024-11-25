cmake_minimum_required(VERSION 3.28)
project(so_i_24_1v6n_2 C)

set(CMAKE_C_STANDARD 11)

include_directories(include)

# Ruta al archivo conan_toolchain.cmake
if(EXISTS "${CMAKE_BINARY_DIR}/../Descargas/TP2/build/Debug/generators/conan_toolchain.cmake")
    include(${CMAKE_BINARY_DIR}/../Descargas/TP2/build/Debug/generators/conan_toolchain.cmake)
else()
    message(FATAL_ERROR "No se encontró el archivo conan_toolchain.cmake en ${CMAKE_BINARY_DIR}/../Descargas/TP2/build/Debug/generators")
endif()

# Buscar las librerías requeridas
find_library(PROM_LIB prom REQUIRED)
find_library(PROMHTTP_LIB promhttp REQUIRED)
find_library(MICROHTTPD_LIB microhttpd REQUIRED)

add_executable(so_i_24_1v6n_2
    include/expose_metrics.h
    include/metrics.h
    src/expose_metrics.c
    src/main.c
    src/metrics.c
)

# Vincular las librerías
target_link_libraries(so_i_24_1v6n_2 ${PROM_LIB} ${PROMHTTP_LIB} ${MICROHTTPD_LIB} pthread)
