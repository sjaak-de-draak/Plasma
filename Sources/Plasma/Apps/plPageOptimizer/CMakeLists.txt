set(plPageOptimizer_SOURCES
    main.cpp
    plAllCreatables.cpp
    plPageOptimizer.cpp
)

set(plPageOptimizer_HEADERS
    plPageOptimizer.h
)

add_executable(plPageOptimizer ${plPageOptimizer_SOURCES})

target_link_libraries(plPageOptimizer CoreLib)
target_link_libraries(plPageOptimizer plResMgr)
target_link_libraries(plPageOptimizer pnUUID)
target_link_libraries(plPageOptimizer ${STRING_THEORY_LIBRARIES})

if(USE_VLD)
    target_link_libraries(plPageOptimizer ${VLD_LIBRARY})
endif()

install(
    TARGETS plPageOptimizer
    DESTINATION tools_cli
)

source_group("Source Files" FILES ${plPageOptimizer_SOURCES})
source_group("Header Files" FILES ${plPageOptimizer_HEADERS})
