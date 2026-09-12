cmake_minimum_required(VERSION 3.20)
project(KIYAMET-DB CXX)
set(CMAKE_CXX_STANDARD 23)
set(CMAKE_CXX_FLAGS "-O3 -march=native -msse4.2 -mclwb")

find_library(IBVERBS ibverbs REQUIRED)
find_library(RDMACM rdmacm REQUIRED)

add_executable(pnet_replica src/pnet_replica.cpp)
add_executable(pnet_recover src/pnet_recover_cluster.cpp)

target_include_directories(pnet_replica PRIVATE include)
target_include_directories(pnet_recover PRIVATE include)
target_link_libraries(pnet_replica ${IBVERBS} ${RDMACM})
target_link_libraries(pnet_recover ${IBVERBS} ${RDMACM})
