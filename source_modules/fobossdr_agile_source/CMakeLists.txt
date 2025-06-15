cmake_minimum_required(VERSION 3.13)
project(fobossdr_agile_source)

file(GLOB SRC "src/*.cpp")

include(${SDRPP_MODULE_CMAKE})

if (MSVC)
    # Lib path
    # TODO...
    target_link_directories(fobossdr_agile_source PRIVATE "C:/Program Files/RigExpert/Fobos/lib/")
    target_include_directories(fobossdr_agile_source PRIVATE "C:/Program Files/RigExpert/Fobos/include/")
    target_link_libraries(fobossdr_agile_source PRIVATE fobos_sdr)
else (MSVC)
    find_package(PkgConfig)

    pkg_check_modules(LIBFOBOS_SDR REQUIRED libfobos_sdr)

    target_include_directories(fobossdr_agile_source PRIVATE ${LIBFOBOS_SDR_INCLUDE_DIRS})
    target_link_directories(fobossdr_agile_source PRIVATE ${LIBFOBOS_SDR_LIBRARY_DIRS})
    target_link_libraries(fobossdr_agile_source PRIVATE ${LIBFOBOS_SDR_LIBRARIES})
endif ()
