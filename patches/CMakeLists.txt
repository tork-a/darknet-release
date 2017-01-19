cmake_minimum_required(VERSION 2.8.3)
project(darknet)

#https://github.com/pjreddie/darknet/pull/6
include(cmake/CMakeLists.txt)

## CATKIN ###
find_package(catkin REQUIRED)

# set variable for darknet-extras.cmake
set(ADD_DARKNET_DEFINITIONS_COMPILE_FLAGS_STRING "")
foreach(DEF ${CUDA_NVCC_DEFINITIONS})
  set(ADD_DARKNET_DEFINITIONS_COMPILE_FLAGS_STRING "${ADD_DARKNET_DEFINITIONS_COMPILE_FLAGS_STRING} -D${DEF}")
endforeach()
foreach(DIR ${CUDA_INCLUDE_DIRS})
  set(ADD_DARKNET_DEFINITIONS_COMPILE_FLAGS_STRING "${ADD_DARKNET_DEFINITIONS_COMPILE_FLAGS_STRING} -I${DIR}")
endforeach()
foreach(DIR ${OpenCV_INCLUDE_DIRS})
  set(ADD_DARKNET_DEFINITIONS_COMPILE_FLAGS_STRING "${ADD_DARKNET_DEFINITIONS_COMPILE_FLAGS_STRING} -I${DIR}")
endforeach()
set(LIBRARIES_STRING "")
foreach(LIB ${LIBRARIES})
  set(ADD_DARKNET_DEFINITIONS_LIBRARIES_STRING "${ADD_DARKNET_DEFINITIONS_LIBRARIES_STRING} ${LIB}")
endforeach()

catkin_package(
  LIBRARIES dnl
  CFG_EXTRAS darknet-extras.cmake)

# download weights
function(download_weights network_name)
  if(NOT EXISTS ${PROJECT_SOURCE_DIR}/weights/${network_name}.weights)
    message(STATUS "DARKNET: Download weights ${network_name}")
    file(DOWNLOAD http://pjreddie.com/media/files/${network_name}.weights
      ${PROJECT_SOURCE_DIR}/weights/${network_name}.weights
      TIMEOUT 120)
  else()
    message(STATUS "DARKNET: Using caced weights ${PROJECT_SOURCE_DIR}/weights/${network_name}.weights")
  endif()
endfunction()

# download pre-trained weights
download_weights(yolo)
# download_weights(tiny-yolo-voc)
# download_weights(yolo-voc)

### INSTALL ###
install(DIRECTORY weights data cfg
  DESTINATION share/darknet
  USE_SOURCE_PERMISSIONS)
install(DIRECTORY src/
  DESTINATION include/darknet
  FILES_MATCHING PATTERN "*.h")
install(TARGETS darknet DESTINATION bin)
install(TARGETS dnl     DESTINATION lib)


### TEST ###
# if(CATKIN_ENABLE_TESTING)
#   find_package(rostest REQUIRED)
#   catkin_add_nosetests(test)
# endif()

