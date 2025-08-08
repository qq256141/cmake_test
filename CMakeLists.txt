cmake_minimum_required(VERSION 3.20)
project(planning)
set(CMAKE_CXX_STANDARD 11)

set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${PROJECT_SOURCE_DIR}/bin)#将动态库和exe文件都指定到bin目录下
#CMAKE_LIBRARY_OUTPUT_DIRECTORY指定动态库的输出目录linux下
#CMAKE_ARCHIVE_OUTPUT_DIRECTORY指定静态库的输出目录
aux_source_directory(${PROJECT_SOURCE_DIR}/src SRC_LIST)#获取src目录下的所有源文件
add_library(common
SHARED 
${SRC_LIST})#生成动态库

target_include_directories(common 
PUBLIC
${PROJECT_SOURCE_DIR}/include)
#让动态库common中的.cpp文件能够找到.h文件
include_directories(${PROJECT_SOURCE_DIR}/include)#头文件地址
#set(EXECUTABLE_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/bin) 可以去掉

add_executable(planning_main planning_main.cpp)#让可执行文件去链接动态库
target_include_directories(planning_main
PUBLIC
${PROJECT_SOURCE_DIR}/include
)#让可执行文件planning_main.cpp能够找到.h文件

target_link_libraries(planning_main 
PUBLIC
common)#链接动态库common 动态库要和可执行文件在同一目录下动态库是.lib文件,静态库是.a文件可执行文件是.exe文件