include(ECMMarkAsTest)

set(decorationButtonTest_SRCS
    mockbridge.cpp mockbridge.h
    mockbutton.cpp mockbutton.h
    mockwindow.cpp mockwindow.h
    mockdecoration.cpp mockdecoration.h
    mocksettings.cpp mocksettings.h
    decorationbuttontest.cpp
    )
add_executable(decorationButtonTest ${decorationButtonTest_SRCS})
target_link_libraries(decorationButtonTest gxde-decoration3-x11 gxde-decoration3-x11-private Qt::Test)
add_test(NAME gxde-decoration3-x11-decorationButtonTest COMMAND decorationButtonTest)
ecm_mark_as_test(decorationButtonTest)

set(decorationTest_SRCS
    mockbridge.cpp mockbridge.h
    mockbutton.cpp mockbutton.h
    mockwindow.cpp mockwindow.h
    mockdecoration.cpp mockdecoration.h
    mocksettings.cpp mocksettings.h
    decorationtest.cpp
    )
add_executable(decorationTest ${decorationTest_SRCS})
target_link_libraries(decorationTest gxde-decoration3-x11 gxde-decoration3-x11-private Qt::Test)
add_test(NAME gxde-decoration3-x11-decorationTest COMMAND decorationTest)
ecm_mark_as_test(decorationTest)

set(decorationShadowTest_SRCS
    shadowtest.cpp
    )
add_executable(decorationShadowTest ${decorationShadowTest_SRCS})
target_link_libraries(decorationShadowTest gxde-decoration3-x11 Qt::Test)
add_test(NAME gxde-decoration3-x11-decorationShadowTest COMMAND decorationShadowTest)
ecm_mark_as_test(decorationShadowTest)
