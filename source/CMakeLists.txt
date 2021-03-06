#   Copyright 2016 Comcast Cable Communications Management, LLC
#
#   Licensed under the Apache License, Version 2.0 (the "License");
#   you may not use this file except in compliance with the License.
#   You may obtain a copy of the License at
#
#       http://www.apache.org/licenses/LICENSE-2.0
#
#   Unless required by applicable law or agreed to in writing, software
#   distributed under the License is distributed on an "AS IS" BASIS,
#   WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
#   See the License for the specific language governing permissions and
#   limitations under the License.

set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -D_ANSC_LINUX ")
set(SOURCES broadband/ssp_messagebus_interface.c broadband/ssp_main.c broadband/ssp_action.c broadband/cosa_webpa_dml.c broadband/cosa_webpa_internal.c broadband/cosa_webpa_apis.c broadband/plugin_main.c broadband/webpa_adapter.c broadband/webpa_internal.c broadband/webpa_table.c broadband/webpa_parameter.c broadband/webpa_attribute.c broadband/webpa_notification.c app/main.c app/libpd.c)
set(HEADERS app/libpd.h)
add_executable(webpa ${SOURCES} ${HEADERS})
set(COMMON_LIBS -ldbus-1 -lccsp_common -lwrp-c -lpthread -lwdmp-c -lmsgpackc -ltrower-base64 -lm -lnanomsg -lcjson -lrt -luuid -llibparodus -lcimplog)
if (BUILD_YOCTO)
set(COMMON_LIBS "${COMMON_LIBS} -llog4c -lrdkloggers")
endif()
target_link_libraries (webpa ${CMAKE_THREAD_LIBS_INIT} ${COMMON_LIBS})
install (TARGETS webpa DESTINATION bin)
