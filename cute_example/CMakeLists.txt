cmake_minimum_required(VERSION 3.19 FATAL_ERROR)

# set(CMAKE_CUDA_FLAGS sm75)
set(CMAKE_CXX_STANDARD 17)
# find_package(CUDA REQUIRED)
project(cute_test CXX C CUDA)


set(CUTLASS_ENABLE_CUBLAS ON CACHE BOOL "cuBLAS usage for tests")

message(STATUS "CMAKE_CURRENT_SOURCE_DIR: ${CMAKE_CURRENT_SOURCE_DIR}")
# message(${CMAKE_CURRENT_SOURCE_DIR})

# include(${CMAKE_CURRENT_SOURCE_DIR}/cuBLAS.cmake)


# message(STATUS "cuda version: " ${CUDA_VERSION_STRING})
add_executable(sgemm_nt_1 sgemm_nt_1.cu)

set_property(TARGET sgemm_nt_1 PROPERTY CUDA_ARCHITECTURES 75)
# string(APPEND CMAKE_CUDA_FLAGS " -gencode arch=compute_75,code=sm_75")
# target_compile_options(sgemm_nt_1 PRIVATE $<$<COMPILE_LANGUAGE:CUDA>:-gencode arch=compute_75,code=sm_75>)
target_include_directories(sgemm_nt_1 PUBLIC /home/mengran/code/cutlass/include)
target_include_directories(sgemm_nt_1 PUBLIC /home/mengran/code/cutlass/tools/util/include)
target_link_libraries(sgemm_nt_1 PUBLIC -lcublas)
# include_directories(/home/mengran/code/cutlass/include)

if (CUTLASS_ENABLE_CUBLAS)
  target_compile_definitions(sgemm_nt_1 PUBLIC  CUTLASS_ENABLE_CUBLAS)
endif()


message(STATUS "final CUTLASS_ENABLE_CUBLAS: ${CUTLASS_ENABLE_CUBLAS}")



