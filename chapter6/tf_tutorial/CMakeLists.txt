cmake_minimum_required(VERSION 2.8.3)
project(tf_tutorial)
find_package(catkin REQUIRED COMPONENTS
  roscpp
  rospy
  tf
  tf2
  tf2_ros
)

catkin_package(
#  INCLUDE_DIRS include
#  LIBRARIES tf_tutorial
   CATKIN_DEPENDS roscpp rospy tf2
#  DEPENDS system_lib
)

###########
## Build ##
###########


include_directories(
# include
  ${catkin_INCLUDE_DIRS}
)

add_executable(tf_broadcaster src/tf_broadcaster.cpp)
target_link_libraries(tf_broadcaster ${catkin_LIBRARIES})

add_executable(tf2_broadcaster src/tf2_broadcaster.cpp)
target_link_libraries(tf2_broadcaster ${catkin_LIBRARIES})

add_executable(tf2_static_broadcaster src/tf2_static_broadcaster.cpp)
target_link_libraries(tf2_static_broadcaster ${catkin_LIBRARIES})

add_executable(tf_listener src/tf_listener.cpp)
target_link_libraries(tf_listener ${catkin_LIBRARIES})

add_executable(tf2_listener src/tf2_listener.cpp)
target_link_libraries(tf2_listener ${catkin_LIBRARIES})

#############
## Install ##
#############
foreach(dir launch rviz)
  install(DIRECTORY ${dir}/
    DESTINATION ${CATKIN_PACKAGE_SHARE_DESTINATION}/${dir})
endforeach(dir)


#############
## Testing ##
#############
if (CATKIN_ENABLE_TESTING)
  find_package(roslaunch REQUIRED)
  roslaunch_add_file_check(launch)
endif()
