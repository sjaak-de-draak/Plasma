set(pnUUID_SOURCES
    pnUUID.cpp
)

if(WIN32)
    set(pnUUID_SOURCES ${pnUUID_SOURCES} pnUUID_Win32.cpp)
endif(WIN32)

if(UNIX)
    if(NOT APPLE)
        find_package(Uuid REQUIRED)
        set_package_properties(Uuid PROPERTIES
            DESCRIPTION "UUID library for Linux (provided by util-linux)"
            TYPE REQUIRED
        )

        include_directories(${Uuid_INCLUDE_DIR})
    endif()

    set(pnUUID_SOURCES ${pnUUID_SOURCES} pnUUID_Unix.cpp)
endif(UNIX)

set(pnUUID_HEADERS
    pnUUID.h
)

add_library(pnUUID STATIC ${pnUUID_SOURCES} ${pnUUID_HEADERS})
target_link_libraries(
    pnUUID
    PUBLIC
        CoreLib
        string_theory
    PRIVATE
        $<$<PLATFORM_ID:Linux>:${Uuid_LIBRARIES}>
        $<$<PLATFORM_ID:Windows>:rpcrt4>
)

source_group("Source Files" FILES ${pnUUID_SOURCES})
source_group("Header Files" FILES ${pnUUID_HEADERS})
