cmake_minimum_required(VERSION 3.15)
project(cnn)

set(CMAKE_CXX_STANDARD 17)

include_directories(SYSTEM ${CMAKE_CURRENT_SOURCE_DIR}/include)
find_package(OpenCV REQUIRED)


set(LAYERS_FILES 
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

add_executable(train 
  src/cnn.cpp 
  ${LAYERS_FILES}
)

add_executable(inference
  src/inference.cpp
  ${LAYERS_FILES}
)

add_executable(gradCAM
  src/grad_cam.cpp
  ${LAYERS_FILES}
)

## 设置库文件
target_link_libraries(train     ${OpenCV_LIBS})
target_link_libraries(inference ${OpenCV_LIBS})
target_link_libraries(gradCAM   ${OpenCV_LIBS})
