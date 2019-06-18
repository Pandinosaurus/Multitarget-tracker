cmake_minimum_required (VERSION 3.5)

project(MultitargetTracker)

set(SOURCES
             main.cpp
             VideoExample.cpp
)

set(HEADERS
             MouseExample.h
             VideoExample.h
)

# ----------------------------------------------------------------------------
# добавляем include директории
# ----------------------------------------------------------------------------
INCLUDE_DIRECTORIES(
                    ${PROJECT_SOURCE_DIR}/../src
                    ${PROJECT_SOURCE_DIR}/../src/Detector
                    ${PROJECT_SOURCE_DIR}/../src/Detector/vibe_src
                    ${PROJECT_SOURCE_DIR}/../src/Detector/Subsense
                    ${PROJECT_SOURCE_DIR}/../src/Tracker
                    ${PROJECT_SOURCE_DIR}/../src/Tracker/HungarianAlg
)

set(LIBS
    ${OpenCV_LIBS}
    mtracking
)

if (BUILD_YOLO_LIB)
if (MSVC)
    if("${CMAKE_SIZEOF_VOID_P}" STREQUAL "4")
        set(BIT_SYSTEM x32)
    else()
        set(BIT_SYSTEM x64)
    endif()

    link_directories(${PROJECT_SOURCE_DIR}/../src/Detector/darknet/3rdparty/lib/${BIT_SYSTEM})
endif(MSVC)

    add_definitions(-DBUILD_YOLO_LIB)
endif(BUILD_YOLO_LIB)

ADD_EXECUTABLE(${PROJECT_NAME} ${SOURCES} ${HEADERS})

TARGET_LINK_LIBRARIES(${PROJECT_NAME} ${LIBS})