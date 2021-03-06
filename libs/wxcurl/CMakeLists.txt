cmake_minimum_required(VERSION 3.1)

if (TARGET ocpn::wxcurl)
    return ()
endif ()

if (NOT CMAKE_MODULE_PATH)
  set (CMAKE_MODULE_PATH ${CMAKE_SOURCE_DIR}/cmake)
endif ()

set(SRC
  include/README
  include/curl
  include/curl/curlbuild.h
  include/curl/curlrules.h
  include/curl/easy.h
  include/curl/curl.h
  include/curl/curlbuild.h.in
  include/curl/curlbuild.h.cmake
  include/curl/typecheck-gcc.h
  include/curl/curlver.h
  include/curl/mprintf.h
  include/curl/stdcheaders.h
  include/curl/multi.h
  src/wx/curl
  src/wx/curl/utils.h
  src/wx/curl/http.h
  src/wx/curl/ftp.h
  src/wx/curl/ftptool.h
  src/wx/curl/dialog.h
  src/wx/curl/thread.h
  src/wx/curl/panel.h
  src/wx/curl/base.h
  src/wx/curl/telnet.h
  src/wx/curl/davtool.h
  src/wx/curl/dav.h
  src/utils.cpp
  src/davtool.cpp
  src/ftpparse.cpp
  src/panel.cpp
  src/ftpparse.h
  src/telnet.cpp
  src/ftp.cpp
  src/base.cpp
  src/dialog.cpp
  src/http.cpp
  src/thread.cpp
  src/ftptool.cpp
  src/dav.cpp
)   

# Library is used also in the plugins, so:
set(CMAKE_POSITION_INDEPENDENT_CODE "ON")

add_library(WXCURL STATIC ${SRC})
add_library(ocpn::wxcurl ALIAS WXCURL)

if (CMAKE_CXX_COMPILER_ID MATCHES "Clang|GNU")
  set_property(TARGET ISO8211 PROPERTY COMPILE_FLAGS "-fvisibility=hidden")
endif ()
target_include_directories(WXCURL PUBLIC ${CMAKE_CURRENT_LIST_DIR}/include)
target_include_directories(WXCURL PUBLIC ${CMAKE_CURRENT_LIST_DIR}/src)
target_link_libraries( WXCURL PUBLIC ${CURL_LIBRARIES})

