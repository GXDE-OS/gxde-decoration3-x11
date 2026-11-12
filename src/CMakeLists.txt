add_definitions(-DTRANSLATION_DOMAIN=\"gxde-decoration3-x11\")

add_subdirectory(private)

set(libkdecoration3_SRCS
    decoratedwindow.cpp
    decoratedwindow.h
    decoration.cpp
    decoration.h
    decoration_p.h
    decorationbutton.cpp
    decorationbutton.h
    decorationbutton_p.h
    decorationbuttongroup.cpp
    decorationbuttongroup.h
    decorationbuttongroup_p.h
    decorationdefines.h
    decorationsettings.cpp
    decorationsettings.h
    decorationshadow.cpp
    decorationshadow.h
    decorationshadow_p.h
    decorationthemeprovider.cpp
    decorationthemeprovider.h

)

add_library(gxde-decoration3-x11 SHARED ${libkdecoration3_SRCS})
ecm_generate_export_header(gxde-decoration3-x11
    BASE_NAME KDECORATIONS3
    VERSION ${PROJECT_VERSION}
    EXPORT_FILE_NAME kdecoration3/kdecoration3_export.h
    DEPRECATION_VERSIONS 5.21
    EXCLUDE_DEPRECATED_BEFORE_AND_AT ${EXCLUDE_DEPRECATED_BEFORE_AND_AT}
)

add_library(gxde-decoration3-x11::Decoration ALIAS gxde-decoration3-x11)

target_link_libraries(gxde-decoration3-x11
    PUBLIC
        Qt::Core
        Qt::Gui
    PRIVATE
        gxde-decoration3-x11-private
        KF6::I18n
)

target_include_directories(gxde-decoration3-x11 INTERFACE "$<INSTALL_INTERFACE:${KDECORATION3_INCLUDEDIR}>" )

set_target_properties(gxde-decoration3-x11 PROPERTIES VERSION   ${KDECORATION3_VERSION}
                                               SOVERSION ${KDECORATION3_SOVERSION}
                                               EXPORT_NAME Decoration
)

ecm_generate_headers(KDecoration3_CamelCase_HEADERS
  HEADER_NAMES
    DecoratedWindow
    Decoration
    DecorationButton
    DecorationButtonGroup
    DecorationSettings
    DecorationShadow
    DecorationThemeProvider
    ScaleHelpers
  PREFIX
    KDecoration3
  REQUIRED_HEADERS KDecoration3_HEADERS
)
install(FILES ${KDecoration3_CamelCase_HEADERS}
        DESTINATION ${KDECORATION3_INCLUDEDIR}/KDecoration3
        COMPONENT Devel)

install(TARGETS gxde-decoration3-x11 EXPORT gxde-decoration3-x11Targets ${KDE_INSTALL_TARGETS_DEFAULT_ARGS})

install(
    FILES
        ${CMAKE_CURRENT_BINARY_DIR}/kdecoration3/kdecoration3_export.h
        ${KDecoration3_HEADERS}
        decorationdefines.h
    DESTINATION
        ${KDECORATION3_INCLUDEDIR}/kdecoration3
    COMPONENT
        Devel
)
