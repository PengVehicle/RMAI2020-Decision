project(roborts_decision)
cmake_minimum_required(VERSION 3.1)

set(Torch_PLACE ${CMAKE_CURRENT_SOURCE_DIR}/../../pytorch)

set(CMAKE_CXX_STANDARD 14)
set(CMAKE_MODULE_PATH ${CMAKE_CURRENT_SOURCE_DIR}/cmake_module)
set(CMAKE_BUILD_TYPE Release)


set(Torch_DIR ${Torch_PLACE})

find_package(catkin REQUIRED COMPONENTS
  roscpp
  tf
  nav_msgs
  geometry_msgs
  actionlib
  roborts_common
  roborts_msgs
  roborts_costmap
  )


find_package(Eigen3 REQUIRED)
find_package(ProtoBuf REQUIRED)
find_package(Torch REQUIRED)

include_directories(
  include
  ${catkin_INCLUDE_DIRS}
  ${Torch_PLACE}/include
)

link_directories(
  ${Torch_PLACE}/lib
)





#generate proto files
file(GLOB ProtoFiles "${CMAKE_CURRENT_SOURCE_DIR}/proto/*.proto")
rrts_protobuf_generate_cpp(${CMAKE_CURRENT_SOURCE_DIR}/proto
  DecisionProtoSrc
  DecisionProtoHds
  ${ProtoFiles}
  )


catkin_package()


# decision_node
add_executable(decision_node
  decision_node.cpp
  ${DecisionProtoHds}
  ${DecisionProtoSrc}
  ${TORCH_INCLUDE_DIRS}
  example_behavior/escape_behavior.h
  example_behavior/back_boot_area_behavior.h
  example_behavior/chase_behavior.h
  example_behavior/patrol_behavior.h
  example_behavior/search_behavior.h
  example_behavior/nn_behavior.h
  executor/chassis_executor.cpp
  )

target_link_libraries(decision_node 
  PRIVATE
  ${TORCH_LIBRARIES}
  roborts_costmap
  ${catkin_LIBRARIES}
  #${PROTOBUF_LIBRARIES}
  -lzmq
  )



# blue_master
add_executable(blue_master
  blue_master.cpp
  ${DecisionProtoHds}
  ${DecisionProtoSrc}
  ${TORCH_INCLUDE_DIRS}
  example_behavior/escape_behavior.h
  example_behavior/back_boot_area_behavior.h
  example_behavior/chase_behavior.h
  example_behavior/patrol_behavior.h
  example_behavior/search_behavior.h
  example_behavior/nn_behavior.h
  executor/chassis_executor.cpp
  )

target_link_libraries(blue_master 
  PRIVATE
  ${TORCH_LIBRARIES}
  roborts_costmap
  ${catkin_LIBRARIES}
  #${PROTOBUF_LIBRARIES}
  -lzmq
  )


# blue_wing
add_executable(blue_wing
  blue_wing.cpp
  ${DecisionProtoHds}
  ${DecisionProtoSrc}
  ${TORCH_INCLUDE_DIRS}
  example_behavior/escape_behavior.h
  example_behavior/back_boot_area_behavior.h
  example_behavior/chase_behavior.h
  example_behavior/patrol_behavior.h
  example_behavior/search_behavior.h
  example_behavior/nn_behavior.h
  executor/chassis_executor.cpp
  )

target_link_libraries(blue_wing 
  PRIVATE
  ${TORCH_LIBRARIES}
  roborts_costmap
  ${catkin_LIBRARIES}
  #${PROTOBUF_LIBRARIES}
  -lzmq
  )




# red_master
add_executable(red_master
  red_master.cpp
  ${DecisionProtoHds}
  ${DecisionProtoSrc}
  ${TORCH_INCLUDE_DIRS}
  example_behavior/escape_behavior.h
  example_behavior/back_boot_area_behavior.h
  example_behavior/chase_behavior.h
  example_behavior/patrol_behavior.h
  example_behavior/search_behavior.h
  example_behavior/nn_behavior.h
  executor/chassis_executor.cpp
  )

target_link_libraries(red_master 
  PRIVATE
  ${TORCH_LIBRARIES}
  roborts_costmap
  ${catkin_LIBRARIES}
  #${PROTOBUF_LIBRARIES}
  -lzmq
  )


# red_wing
add_executable(red_wing
  red_wing.cpp
  ${DecisionProtoHds}
  ${DecisionProtoSrc}
  ${TORCH_INCLUDE_DIRS}
  example_behavior/escape_behavior.h
  example_behavior/back_boot_area_behavior.h
  example_behavior/chase_behavior.h
  example_behavior/patrol_behavior.h
  example_behavior/search_behavior.h
  example_behavior/nn_behavior.h
  executor/chassis_executor.cpp
  )

target_link_libraries(red_wing 
  PRIVATE
  ${TORCH_LIBRARIES}
  roborts_costmap
  ${catkin_LIBRARIES}
  #${PROTOBUF_LIBRARIES}
  -lzmq
  )




