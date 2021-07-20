cmake_minimum_required(VERSION 3.5)

project(qtDrawImageLineReg
    #    LANGUAGES CXX
    VERSION   "1.1.2.9" )

set(CMAKE_INCLUDE_CURRENT_DIR ON)

set(CMAKE_AUTOUIC ON)
set(CMAKE_AUTOMOC ON)
set(CMAKE_AUTORCC ON)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# QtCreator supports the following variables for Android, which are identical to qmake Android variables.
# Check http://doc.qt.io/qt-5/deployment-android.html for more information.
# They need to be set before the find_package(Qt5 ...) call.

#if(ANDROID)
#    set(ANDROID_PACKAGE_SOURCE_DIR "${CMAKE_CURRENT_SOURCE_DIR}/android")
#    if (ANDROID_ABI STREQUAL "armeabi-v7a")
#        set(ANDROID_EXTRA_LIBS
#            ${CMAKE_CURRENT_SOURCE_DIR}/path/to/libcrypto.so
#            ${CMAKE_CURRENT_SOURCE_DIR}/path/to/libssl.so)
#    endif()
#endif()

find_package(QT NAMES Qt6 Qt5 COMPONENTS Widgets LinguistTools REQUIRED)
find_package(Qt${QT_VERSION_MAJOR} COMPONENTS Widgets LinguistTools REQUIRED)

set(TS_FILES qtDrawImageLineReg_zh_CN.ts)


if (UNIX)
    set(Eigen3_DIR  "/home/alex/bin2104/eigen-3.3.7/x64/share/eigen3/cmake" )
    find_package(  Eigen3  REQUIRED  PATHS  "/home/alex/bin2104/eigen-3.3.7/x64" )
elseif (MSVC)
    set(Eigen3_DIR  "D:/win10/aspDep14/eigen-3.3.7/x64/share/eigen3/cmake" )
    find_package(  Eigen3  REQUIRED  PATHS  "D:/win10/aspDep14/eigen-3.3.7/x64" )
endif ()
include_directories(  ${EIGEN3_INCLUDE_DIR})
include_directories(  ${EIGEN3_INCLUDE_DIRS})
include_directories(  ${EIGEN3_ROOT_DIR})
include_directories(  "D:/win10/aspDep14/eigen-3.3.7/x64/include/eigen3")



if (UNIX)
    if( 0 )
        set(Opencv_rot_my /home/alex/bin2104/installCv3414Ubun2104FullNew)
        set(OpenCV_DIR ${Opencv_rot_my}/share/OpenCV)
        find_package(opencv PATHS ${Opencv_rot_my}/share/OpenCV) #REQUIRED
        include_directories(${Opencv_rot_my}/include
            ${Opencv_rot_my}/include/opencv
            ${Opencv_rot_my}/include/opencv2
            )
    endif()
    if(0)
        set(Opencv_rot_my /home/alex/bin2104/installCV410Ubun1804GLIPP)
        set(OpenCV_DIR ${Opencv_rot_my}/lib/cmake/opencv4)
        find_package(opencv PATHS ${Opencv_rot_my} ) #REQUIRED
        include_directories(${Opencv_rot_my}/include
            ${Opencv_rot_my}/include/opencv4
            ${Opencv_rot_my}/include/opencv4/opencv2
            )
    endif()
    if(1)  # installCv24136U2104
        set(Opencv_rot_my /home/alex/bin2104/installCv24136U2104)
        set(OpenCV_DIR ${Opencv_rot_my}/share/OpenCV)
        find_package(opencv PATHS ${Opencv_rot_my}/share/OpenCV) #REQUIRED
        include_directories(${Opencv_rot_my}/include
            ${Opencv_rot_my}/include/opencv
            ${Opencv_rot_my}/include/opencv2
            )
    endif()
elseif (MSVC)
    if(0)
        set(Opencv_rot_my  "D:/win10/cv451/opencv/build" REQUIRED)
        set(OpenCV_DIR "D:/win10/cv451/opencv/build/x64/vc14/lib")
        find_package(opencv PATHS ${Opencv_rot_my} ) #REQUIRED
        include_directories(${Opencv_rot_my}/include
            ${Opencv_rot_my}/include/opencv
            ${Opencv_rot_my}/include/opencv2
            )
    endif()
    if(0)  # installCv24136U2104
        set(Opencv_rot_my  "D:/win10/cv24136/opencv/build"    )
        set(OpenCV_DIR ${Opencv_rot_my}/x64/vc14/lib)
        find_package(opencv PATHS ${Opencv_rot_my}  ) #REQUIRED
        include_directories(${Opencv_rot_my}/include
            ${Opencv_rot_my}/include/opencv
            ${Opencv_rot_my}/include/opencv2
            )
    endif()
    if( 1 )  # installCv24136U2104
        set(Opencv_rot_my  "D:/win10/cv342/opencv/build"    )
        set(OpenCV_DIR ${Opencv_rot_my}/x64/vc14/lib)
        find_package(opencv PATHS ${Opencv_rot_my}  ) #REQUIRED
        include_directories(${Opencv_rot_my}/include
            ${Opencv_rot_my}/include/opencv
            ${Opencv_rot_my}/include/opencv2
            )
        endif ()
endif ()
link_directories(${Opencv_rot_my}/lib)


if (UNIX)
    include_directories("/home/alex/bin2104/halcon-19.11.0.0-linux/include/halconcpp"
        "/home/alex/bin2104/halcon-19.11.0.0-linux/include")
    link_directories("/home/alex/bin2104/halcon-19.11.0.0-linux/lib/x64-linux")
elseif (MSVC)
    include_directories("D:/Program Files/MVTec/HALCON-17.12-Progress/include/halconcpp"
        "D:/Program Files/MVTec/HALCON-17.12-Progress/include")
    link_directories("D:/Program Files/MVTec/HALCON-17.12-Progress/lib/x64-win64")
endif ()


include_directories(  "../SDL2-devel-2.0.12-VC/include" )
link_directories(  "../SDL2-devel-2.0.12-VC/lib/x64")


include_directories("../ffmpeg-4.0-win64-dev/include" )
link_directories(  "../ffmpeg-4.0-win64-dev/lib")


if (UNIX)
    set(LIBS_RELATED ${OpenCV_LIBS}
        libopencv_core.so libopencv_highgui.so libopencv_imgcodecs.so
        libopencv_imgproc.so libopencv_videoio.so libopencv_ml.so
        libopencv_features2d.so libopencv_flann.so libopencv_objdetect.so
        -lopencv_nonfree
        -lopencv_contrib
        #    -lpng  -lthread -ljpeg  -lpng16
        #     nlohmann_json::nlohmann_json        #     tinyxml2::tinyxml2
        #     glog::glog
        -lhalconcpp -lhalcon
        #            -lXext -lX11 -ldl -lpthread
        )
elseif (MSVC)
    set(LIBS_RELATED ${OpenCV_LIBS}
        #    -lpng  -lthread -ljpeg  -lpng16
        #     nlohmann_json::nlohmann_json
        #     tinyxml2::tinyxml2
        #     glog::glog
        -lhalconcpp -lhalcon
        #        -lXext -lX11 -ldl -lpthread
        -lSDL2
        -lavdevice -lavcodec.dll
        )
endif ()


#set(HEADERS  data.h  rpm.h  )

aux_source_directory(  ./    sources_all )
aux_source_directory(  ./GIFmaker    sources_all )
aux_source_directory(  ./halconCompare    sources_all )
include_directories( ./ ./GIFmaker  ./halconCompare  )




if(ANDROID)
    add_library(qtDrawImageLineReg SHARED
        main.cpp        widget.cpp        widget.h        widget.ui
        ${TS_FILES}
        )
else()
    add_executable(qtDrawImageLineReg
        #        main.cpp#        widget.cpp#        widget.h#        widget.ui
        ${TS_FILES}  ${HEADERS}  ${sources_all}  QTPlayer.qrc
        #        formmainapp.h    formmainapp.cpp  formmainapp.ui
        )
endif()

target_link_libraries(qtDrawImageLineReg PRIVATE Qt${QT_VERSION_MAJOR}::Widgets
    ${LIBS_RELATED}
    )

qt5_create_translation(QM_FILES ${CMAKE_SOURCE_DIR} ${TS_FILES})




set(EXECUTABLE_OUTPUT_PATH   ${CMAKE_BINARY_DIR}/../bin_release_VC14_ver_debug  )
#set(LIBRARY_OUTPUT_PATH ${CMAKE_BINARY_DIR}/../bin)
#set(EXECUTABLE_OUTPUT_PATH ${CMAKE_BINARY_DIR}/../bin)
#set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/../bin)
#set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/../lib)


#-------------------install  destation ---------------------------
#set( DESTINATION  "../install/")
set(CMAKE_INSTALL_PREFIX "../install/")
#          And to the end of the top-level CMakeLists.txt we add:
install(TARGETS ${PROJECT_NAME} DESTINATION bin)
#install(FILES "${PROJECT_BINARY_DIR}/TutorialConfig.h"  DESTINATION include  )


if (0)
    #
    # Format the project using the `clang-format` target (i.e: cmake --build build --target clang-format)
    #

    #add_clang_format_target()

    #
    # Install library for easy downstream inclusion
    #

    include(GNUInstallDirs)
    install(
        TARGETS
        ${PROJECT_NAME}
        EXPORT
        ${PROJECT_NAME}Targets
        LIBRARY DESTINATION
        ${CMAKE_INSTALL_LIBDIR}
        RUNTIME DESTINATION
        ${CMAKE_INSTALL_BINDIR}
        ARCHIVE DESTINATION
        ${CMAKE_INSTALL_LIBDIR}
        INCLUDES DESTINATION
        include
        PUBLIC_HEADER DESTINATION
        include
        )

    install(
        EXPORT
        ${PROJECT_NAME}Targets
        FILE
        ${PROJECT_NAME}Targets.cmake
        NAMESPACE
        ${PROJECT_NAME}::
        DESTINATION
        ${CMAKE_INSTALL_LIBDIR}/cmake/${PROJECT_NAME}
        )

    #
    # Add version header
    #

    configure_file(
        ${CMAKE_CURRENT_LIST_DIR}/cmake/version.hpp.in
        include/${PROJECT_NAME_LOWERCASE}/version.hpp
        @ONLY
        )

    install(
        FILES
        ${CMAKE_CURRENT_BINARY_DIR}/include/${PROJECT_NAME_LOWERCASE}/version.hpp
        DESTINATION
        include/${PROJECT_NAME_LOWERCASE}
        )

    #
    # Install the `include` directory
    #

    #install(
    #    DIRECTORY
    ##    include/${PROJECT_NAME_LOWERCASE}
    #    BasicDef/${PROJECT_NAME_LOWERCASE}
    #     exportApi/${PROJECT_NAME_LOWERCASE}
    #     DESTINATION
    #    include
    #    )

    install(
        FILES
        #    include/${PROJECT_NAME_LOWERCASE}
        BasicDef/${PROJECT_NAME_LOWERCASE}/skd_vision_basic.h
        BasicDef/${PROJECT_NAME_LOWERCASE}/SKDVISION_global.h
        exportApi/${PROJECT_NAME_LOWERCASE}/api_vision.h
        #     exportApi/${PROJECT_NAME_LOWERCASE}
        DESTINATION
        include
        )


    #verbose_message("Install targets succesfully build. Install with `cmake --build <build_directory> --target install --config <build_config>`.")

    #
    # Quick `ConfigVersion.cmake` creation
    #

    include(CMakePackageConfigHelpers)
    write_basic_package_version_file(
        ${PROJECT_NAME}ConfigVersion.cmake
        VERSION
        ${PROJECT_VERSION}
        COMPATIBILITY
        SameMajorVersion
        )

    configure_package_config_file(
        ${CMAKE_CURRENT_LIST_DIR}/cmake/${PROJECT_NAME}Config.cmake.in
        ${CMAKE_CURRENT_BINARY_DIR}/${PROJECT_NAME}Config.cmake
        INSTALL_DESTINATION
        ${CMAKE_INSTALL_LIBDIR}/cmake/${PROJECT_NAME}
        )

    install(
        FILES
        ${CMAKE_CURRENT_BINARY_DIR}/${PROJECT_NAME}Config.cmake
        ${CMAKE_CURRENT_BINARY_DIR}/${PROJECT_NAME}ConfigVersion.cmake
        DESTINATION
        ${CMAKE_INSTALL_LIBDIR}/cmake/${PROJECT_NAME}
        )

    #
    # Generate export header if specified
    #

    if (${PROJECT_NAME}_GENERATE_EXPORT_HEADER)
        include(GenerateExportHeader)
        generate_export_header(${PROJECT_NAME})
        install(
            FILES
            ${PROJECT_BINARY_DIR}/${PROJECT_NAME_LOWERCASE}_export.h
            DESTINATION
            include
            )
        message(STATUS "Generated the export header `${PROJECT_NAME_LOWERCASE}_export.h` and installed it.")
    endif ()

    message(STATUS "Finished building requirements for installing the package.\n")

    #
    # Unit testing setup
    #
    if (0)
        if (${PROJECT_NAME}_ENABLE_UNIT_TESTING)
            enable_testing()
            message(STATUS "Build unit tests for the project. Tests should always be found in the test folder\n")
            add_subdirectory(test)
        endif ()
    endif ()


endif ()



