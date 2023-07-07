cmake_minimum_required(VERSION 3.16)

project(qml_same_names VERSION 0.1 LANGUAGES CXX)

set(CMAKE_CXX_STANDARD_REQUIRED ON)

find_package(Qt6 6.5 REQUIRED COMPONENTS Quick)

qt_standard_project_setup(REQUIRES 6.5)

qt_add_executable(appqml_same_names
    main.cpp
)

qt_add_qml_module(appqml_same_names
    URI qml_same_names
    VERSION 1.0
    QML_FILES Main.qml
    page1/LeftBar.qml
    page2/LeftBar.qml # Comment this line to make app work
)

set_target_properties(appqml_same_names PROPERTIES
    MACOSX_BUNDLE_GUI_IDENTIFIER my.example.com
    MACOSX_BUNDLE_BUNDLE_VERSION ${PROJECT_VERSION}
    MACOSX_BUNDLE_SHORT_VERSION_STRING ${PROJECT_VERSION_MAJOR}.${PROJECT_VERSION_MINOR}
    MACOSX_BUNDLE TRUE
    WIN32_EXECUTABLE TRUE
)

target_link_libraries(appqml_same_names
    PRIVATE Qt6::Quick
)

install(TARGETS appqml_same_names
    BUNDLE DESTINATION .
    LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR}
    RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR}
)
