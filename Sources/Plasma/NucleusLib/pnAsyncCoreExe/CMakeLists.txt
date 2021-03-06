set(pnAsyncCoreExe_SOURCES
    pnAceCore.cpp
    pnAceIo.cpp
    pnAceThread.cpp
    pnAceTimer.cpp
)

set(pnAsyncCoreExe_HEADERS
    Pch.h
)

set(pnAysncCoreExe_PRIVATE
    Private/pnAceInt.h
)

# I would do platform specific stuff here,
# but Pch.h just includes everything, so...

set(pnAysncCoreExe_PRIVATE_NT
    Private/Nt/pnAceNt.cpp
    Private/Nt/pnAceNt.h
    Private/Nt/pnAceNtInt.h
    Private/Nt/pnAceNtSocket.cpp
    Private/Nt/pnAceNtThread.cpp
)

set(pnAsyncCoreExe_PRIVATE_UNIX
    Private/Unix/pnAceUx.h
)

set(pnAsyncCoreExe_PRIVATE_WIN32
    Private/Win32/pnAceW32Dns.cpp
    Private/Win32/pnAceW32Thread.cpp
)

# End questionable part

add_library(pnAsyncCoreExe STATIC
            ${pnAsyncCoreExe_SOURCES} ${pnAsyncCoreExe_HEADERS}
            ${pnAsyncCoreExe_PRIVATE} ${pnAysncCoreExe_PRIVATE_NT}
            ${pnAsyncCoreExe_PRIVATE_UNIX} ${pnAsyncCoreExe_PRIVATE_WIN32})

target_link_libraries(
    pnAsyncCoreExe
    PUBLIC
        CoreLib
        pnAsyncCore
        pnNetBase
        pnUtils
)
if(USE_VLD)
    target_link_libraries(pnAsyncCoreExe PRIVATE ${VLD_LIBRARY})
endif()

source_group("Source Files" FILES ${pnAsyncCoreExe_SOURCES})
source_group("Header Files" FILES ${pnAsyncCoreExe_HEADERS})
source_group("Private" FILES ${pnAsyncCoreExe_PRIVATE})
source_group("Private\\Nt" FILES ${pnAysncCoreExe_PRIVATE_NT})
source_group("Private\\Unix" FILES ${pnAsyncCoreExe_PRIVATE_UNIX})
source_group("Private\\Win32" FILES ${pnAsyncCoreExe_PRIVATE_WIN32})
