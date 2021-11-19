cmake_minimum_required(VERSION 2.8)

project(usb_monitor)

list(APPEND CMAKE_PREFIX_PATH "/usr/local/viper/")

include_directories(/usr/local/viper/include/)
link_directories(/usr/local/viper/lib/)

include_directories(/usr/include/)
link_directories(/usr/lib/x86_64-linux-gnu/)

find_package(PkgConfig REQUIRED)
find_package(jsoncpp REQUIRED)
# find_package(UDev REQUIRED)
pkg_check_modules(UDEV REQUIRED libudev)

include_directories(
    ${JSONCPP_INCLUDE_DIRS}
    ${UDEV_INCLUDE_DIRS}
    jsoncpp
)

set(SOURCE_DIR "src")
set(SOURCES
    ${SOURCE_DIR}/main.cpp
    ${SOURCE_DIR}/udev.cpp
    ${SOURCE_DIR}/usb_monitor.cpp
    ${SOURCE_DIR}/utils.cpp)
# set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -O3 -ludev -pipe")

add_executable(${PROJECT_NAME} ${SOURCES})

# link_libraries(${JSONCPP_LIBRARIES})

target_link_libraries(
    ${PROJECT_NAME}

    ${UDEV_LIBRARIES}
    ${JSONCPP_LIBRARIES}
    jsoncpp
)
