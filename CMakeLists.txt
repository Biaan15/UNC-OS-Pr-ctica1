cmake_minimum_required(VERSION 3.10)
project(so-i-24-chp2-Biaan15)

# Establecer el tipo de construcción por defecto
if(NOT CMAKE_BUILD_TYPE)
    set(CMAKE_BUILD_TYPE Release) 
endif()

# Ruta al archivo conan_toolchain.cmake usando CMAKE_BINARY_DIR
set(CONAN_TOOLCHAIN_FILE "${CMAKE_BINARY_DIR}/../Descargas/TP2/build/Debug/generators/conan_toolchain.cmake")
message(STATUS "Conan toolchain file: ${CONAN_TOOLCHAIN_FILE}")

# Incluir el archivo conan_toolchain.cmake si existe, de lo contrario mostrar un mensaje de error
if(EXISTS ${CONAN_TOOLCHAIN_FILE})
    include(${CONAN_TOOLCHAIN_FILE})
else()
    message(FATAL_ERROR "No se encontró el archivo ${CONAN_TOOLCHAIN_FILE}")
endif()

# Incluir directorios de encabezados
include_directories(${CMAKE_SOURCE_DIR}/include)
include_directories(${CMAKE_SOURCE_DIR}/lib)
include_directories(${CONAN_INCLUDE_DIRS}) 

# Añadir el ejecutable
add_executable(so-i-24-chp2-Biaan15
    src/main.c
    src/metrics.c
    src/expose_metrics.c
    src/config.c
)

add_library(so-i-24-chp2-Biaan15lib STATIC
    src/metrics.c
    src/expose_metrics.c
    src/config.c
)

# Añadir el directorio donde se instalan las librerías compartidas (instaladas con sudo make install)
link_directories(/usr/local/lib)

target_link_libraries(so-i-24-chp2-Biaan15 PRIVATE so-i-24-chp2-Biaan15_lib)

find_package(cJSON REQUIRED)

# Vincular las librerías libprom y libpromhttp desde /usr/local/lib
target_link_libraries(so-i-24-chp2-Biaan15_lib
    /usr/local/lib/libprom.so
    /usr/local/lib/libpromhttp.so
    cjson::cjson
)
