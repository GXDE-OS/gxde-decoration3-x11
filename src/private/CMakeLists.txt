set(libkdecoration3Private_SRCS
    decoratedwindowprivate.cpp
    decoratedwindowprivate.h
    decorationbridge.cpp
    decorationbridge.h
    decorationsettingsprivate.cpp
    decorationsettingsprivate.h
)

add_library(gxde-decoration3-x11-private SHARED ${libkdecoration3Private_SRCS})

generate_export_header(
    gxde-decoration3-x11-private
BASE_NAME
    KDECORATIONS_PRIVATE
EXPORT_FILE_NAME
    kdecoration3/private/kdecoration3_private_export.h
)

add_library(gxde-decoration3-x11::DecorationPrivate ALIAS gxde-decoration3-x11-private)

target_link_libraries(gxde-decoration3-x11-private
    PUBLIC
        Qt::Core
        Qt::Gui
)

target_include_directories(gxde-decoration3-x11-private INTERFACE "$<INSTALL_INTERFACE:${KDECORATION3_INCLUDEDIR}>" )

set_target_properties(gxde-decoration3-x11-private PROPERTIES VERSION   ${KDECORATION3_VERSION}
                                                      SOVERSION 2
                                                      EXPORT_NAME DecorationPrivate
)

ecm_generate_headers(KDecoration3Private_CamelCase_HEADERS
  HEADER_NAMES
    DecoratedWindowPrivate
    DecorationBridge
    DecorationSettingsPrivate
  PREFIX
    KDecoration3/Private
  REQUIRED_HEADERS KDecoration3Private_HEADERS
)
install(FILES ${KDecoration3Private_CamelCase_HEADERS}
        DESTINATION ${KDECORATION3_INCLUDEDIR}/KDecoration3/Private
        COMPONENT Devel)

install(TARGETS gxde-decoration3-x11-private EXPORT gxde-decoration3-x11Targets ${KDE_INSTALL_TARGETS_DEFAULT_ARGS})

install(
    FILES
        ${CMAKE_CURRENT_BINARY_DIR}/kdecoration3/private/kdecoration3_private_export.h
        ${KDecoration3Private_HEADERS}
    DESTINATION
        ${KDECORATION3_INCLUDEDIR}/kdecoration3/private
    COMPONENT
        Devel
)
