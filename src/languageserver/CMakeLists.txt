# Copyright (C) 2022 The Qt Company Ltd.
# SPDX-License-Identifier: BSD-3-Clause

#####################################################################
## LanguageServer Module:
#####################################################################

qt_internal_add_module(LanguageServerPrivate
    INTERNAL_MODULE
    SOURCES
      qlanguageserverprespectypes_p.h
      qlanguageserverspec_p.h
      qlanguageserverspectypes_p.h
      qlanguageserverjsonrpctransport_p.h qlanguageserverjsonrpctransport.cpp
      qtlanguageserverglobal.h
      qlanguageserverbase_p.h qlanguageserverbase_p_p.h qlanguageserverbase.cpp
      qlanguageservergen_p.h qlanguageservergen_p_p.h qlanguageservergen.cpp
      qlanguageserverprotocol_p.h qlanguageserverprotocol.cpp
      qlspnotifysignals_p.h qlspnotifysignals.cpp
      qlspcustomtypes_p.h
    DEFINES
        QT_BUILD_LANGUAGESERVER_LIB
    PUBLIC_LIBRARIES
        Qt::CorePrivate
        Qt::JsonRpcPrivate
)

# remember to use this function! Otherwise it will throw weird linker errors
function(link_qtlanguageserver tar)
  target_sources(${tar} PRIVATE qlanguageserver_p.h qlanguageserver_p_p.h qlanguageserver.cpp)
  target_link_libraries(${tar} PRIVATE Qt::LanguageServerPrivate)
endfunction()

if(MSVC)
  set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} /bigobj")
elseif (MINGW)
  set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wa,-mbig-obj")
endif()
