############################################################################
# <summary> CMakeLists.txt for OpenCV and CUDA. </summary>
# <date>    2012-02-07          </date>
# <author>  Quan Tran Minh. edit by Johannes Kast, Michael Sarahan </author>
# <email>   quantm@unist.ac.kr  kast.jo@googlemail.com msarahan@gmail.com</email>
############################################################################
# minimum required cmake version
cmake_minimum_required(VERSION 3.20)
project(ProblemSet3 LANGUAGES CUDA CXX)

find_package(CUDA REQUIRED)
find_package(OpenCV REQUIRED)

set(CUDA_TOOLKIT_ROOT_DIR "/usr/local/cuda")
set(CMAKE_CUDA_COMPILER "${CUDA_TOOLKIT_ROOT_DIR}/bin/nvcc")
set(CUDA_INCLUDE_DIRS "${CUDA_TOOLKIT_ROOT_DIR}/include")
set(CUDA_CUDART_LIBRARY "${CUDA_TOOLKIT_ROOT_DIR}/lib64/libcudart.so")
set(CMAKE_CUDA_ARCHITECTURES "native")

SET (compare_files compare.cpp)

file( GLOB  hdr *.hpp *.h )
file( GLOB  cu  *.cu)
SET (HW3_files main.cpp loadSaveImage.cpp reference_calc.cpp compare.cpp)
    
add_executable(HW3 ${HW3_files} ${hdr} ${cu})

target_include_directories(HW3 PRIVATE ${CUDA_INCLUDE_DIRS} ${OpenCV_INCLUDE_DIRS})
target_link_libraries(HW3 PRIVATE ${CUDA_CUDART_LIBRARY} ${OpenCV_LIBS})
