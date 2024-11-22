cmake_minimum_required(VERSION 3.10)
project(so-i-24-chp2-Biaan15)

# Establecer el tipo de construcción por defecto
if(NOT CMAKE_BUILD_TYPE)
    set(CMAKE_BUILD_TYPE Release) 
endif()

include(${CMAKE_BINARY_DIR}/conan_toolchain.cmake)

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

