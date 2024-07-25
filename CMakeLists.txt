cmake_minimum_required(VERSION 3.15)
project(cnn)

set(CMAKE_CXX_STANDARD 17)

include_directories(SYSTEM ${CMAKE_CURRENT_SOURCE_DIR}/include)
find_package(OpenCV REQUIRED)


add_library(cnn STATIC
  src/data_format.cpp
  src/pipeline.cpp 
  src/relu.cpp
  src/linear.cpp
  src/conv2d.cpp
  src/func.cpp
  src/pool2d.cpp
  src/batchnorm2d.cpp
  src/metrics.cpp
  src/architectures.cpp
  src/alexnet.cpp
  src/dropout.cpp
)
target_link_libraries(cnn PUBLIC ${OpenCV_LIBS})

add_executable(train 
  src/cnn.cpp
)

add_executable(inference
  src/inference.cpp
)

add_executable(gradCAM
  src/grad_cam.cpp
)

target_link_libraries(train PUBLIC cnn)
target_link_libraries(inference PUBLIC cnn)
target_link_libraries(gradCAM PUBLIC cnn)
