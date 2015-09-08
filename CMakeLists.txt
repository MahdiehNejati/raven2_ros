cmake_minimum_required(VERSION 2.8.3)
project(raven_2)

## Find catkin macros and libraries
## if COMPONENTS list like find_package(catkin REQUIRED COMPONENTS xyz)
## is used, also find other catkin packages
find_package(catkin REQUIRED COMPONENTS
  dynamic_reconfigure
  geometry_msgs
  message_generation
  roscpp
  sensor_msgs
  std_msgs
  tf
  visualization_msgs
)

## System dependencies are found with CMake's conventions
# find_package(Boost REQUIRED COMPONENTS system)


## Uncomment this if the package has a setup.py. This macro ensures
## modules and global scripts declared therein get installed
## See http://ros.org/doc/api/catkin/html/user_guide/setup_dot_py.html
# catkin_python_setup()

################################################
## Declare ROS messages, services and actions ##
################################################

## To declare and build messages, services or actions from within this
## package, follow these steps:
## * Let MSG_DEP_SET be the set of packages whose message types you use in
##   your messages/services/actions (e.g. std_msgs, actionlib_msgs, ...).
## * In the file package.xml:
##   * add a build_depend tag for "message_generation"
##   * add a build_depend and a run_depend tag for each package in MSG_DEP_SET
##   * If MSG_DEP_SET isn't empty the following dependency has been pulled in
##     but can be declared for certainty nonetheless:
##     * add a run_depend tag for "message_runtime"
## * In this file (CMakeLists.txt):
##   * add "message_generation" and every package in MSG_DEP_SET to
##     find_package(catkin REQUIRED COMPONENTS ...)
##   * add "message_runtime" and every package in MSG_DEP_SET to
##     catkin_package(CATKIN_DEPENDS ...)
##   * uncomment the add_*_files sections below as needed
##     and list every .msg/.srv/.action file to be processed
##   * uncomment the generate_messages entry below
##   * add every package in MSG_DEP_SET to generate_messages(DEPENDENCIES ...)


## Generate messages in the 'msg' folder
add_message_files(
  FILES
  raven_automove.msg
  raven_state.msg
)

## Generate services in the 'srv' folder
# add_service_files(
#   FILES
#   Service1.srv
#   Service2.srv
# )

## Generate actions in the 'action' folder
# add_action_files(
#   FILES
#   Action1.action
#   Action2.action
# )

## Generate added messages and services with any dependencies listed here
generate_messages(
  DEPENDENCIES
  std_msgs
  geometry_msgs
)
################################################
## Declare ROS dynamic reconfigure parameters ##
################################################

## To declare and build dynamic reconfigure parameters within this
## package, follow these steps:
## * In the file package.xml:
##   * add a build_depend and a run_depend tag for "dynamic_reconfigure"
## * In this file (CMakeLists.txt):
##   * add "dynamic_reconfigure" to
##     find_package(catkin REQUIRED COMPONENTS ...)
##   * uncomment the "generate_dynamic_reconfigure_options" section below
##     and list every .cfg file to be processed

## Generate dynamic reconfigure parameters in the 'cfg' folder
 generate_dynamic_reconfigure_options(
   cfg/MyStuff.cfg
#   cfg/DynReconf2.cfg
 )

###################################
## catkin specific configuration ##
###################################
## The catkin_package macro generates cmake config files for your package
## Declare things to be passed to dependent projects
## INCLUDE_DIRS: uncomment this if you package contains header files
## LIBRARIES: libraries you create in this project that dependent projects also need
## CATKIN_DEPENDS: catkin_packages dependent projects also need
## DEPENDS: system dependencies of this project that dependent projects also need
catkin_package(
#  INCLUDE_DIRS include
#  LIBRARIES raven_2
#  CATKIN_DEPENDS dynamic_reconfigure geometry_msgs message_runtime roscpp sensor_msgs std_msgs tf visualization_msgs
#  DEPENDS system_lib
)

###########
## Build ##
###########

## Specify additional locations of header files
## Your package locations should be listed before other locations
# include_directories(include)
include_directories(include ${catkin_INCLUDE_DIRS})

## Declare a C++ library
# add_library(raven_2
#   src/${PROJECT_NAME}/raven_2.cpp
# )

## Add cmake target dependencies of the library
## as an example, code may need to be generated before libraries
## either from message generation or dynamic reconfigure
#add_dependencies(raven_2 ${${PROJECT_NAME}_EXPORTED_TARGETS} ${catkin_EXPORTED_TARGETS} ${PROJECT_NAME}_gencfg)
#add_dependencies(dynamic_reconfigure_node ${PROJECT_NAME}_gencfg)

## Declare a C++ executable
# add_executable(raven_2_node src/raven_2_node.cpp)
add_executable(r2_control
#src/raven/asinw.cpp
src/raven/dof.cpp
src/raven/fwd_cable_coupling.cpp
src/raven/fwd_kinematics.cpp
src/raven/r2_kinematics.cpp
src/raven/get_USB_packet.cpp
src/raven/globals.cpp
#src/raven/grasp.cpp
src/raven/grav_comp.cpp
src/raven/hmatrix.cpp
src/raven/init.cpp
src/raven/inv_cable_coupling.cpp
#src/raven/inv_kinematics.cpp
#src/raven/linear_parabolic_traj.cpp
src/raven/local_io.cpp
src/raven/log.cpp
src/raven/mapping.cpp
src/raven/motor.cpp
src/raven/network_layer.cpp
src/raven/overdrive_detect.cpp
src/raven/parallel.cpp
src/raven/pid_control.cpp
src/raven/put_USB_packet.cpp
src/raven/rt_process_preempt.cpp
src/raven/rt_raven.cpp
src/raven/state_estimate.cpp
src/raven/state_machine.cpp
src/raven/homing.cpp
src/raven/trajectory.cpp
src/raven/console_process.cpp
#src/raven/trajectory_gen_ee449.cpp
src/raven/t_to_DAC_val.cpp
src/raven/update_atmel_io.cpp
src/raven/update_device_state.cpp
src/raven/USB_init.cpp
src/raven/utils.cpp
src/raven/reconfigure.cpp
#src/raven/velocity.cpp
src/raven/tools.cpp
)

## Add cmake target dependencies of the executable
## same as for the library above
#### TODO MAHDIEH ###
#add_dependencies(r2_control raven_2_generate_messages_cpp) # ${${PROJECT_NAME}_EXPORTED_TARGETS} ${catkin_EXPORTED_TARGETS})
add_dependencies(r2_control ${catkin_EXPORTED_TARGETS})

## Specify libraries to link a library or executable target against
target_link_libraries(r2_control
  ${catkin_LIBRARIES}
)
# target_link_libraries(${PROJECT_NAME} ${catkin_LIBRARIES} )

#############
## Install ##
#############

# all install targets should use catkin DESTINATION variables
# See http://ros.org/doc/api/catkin/html/adv_user_guide/variables.html

## Mark executable scripts (Python etc.) for installation
## in contrast to setup.py, you can choose the destination
# install(PROGRAMS
#   scripts/my_python_script
#   DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION}
# )

## Mark executables and/or libraries for installation
# install(TARGETS raven_2 raven_2_node
#   ARCHIVE DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
#   LIBRARY DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
#   RUNTIME DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION}
# )

## Mark cpp header files for installation
# install(DIRECTORY include/${PROJECT_NAME}/
#   DESTINATION ${CATKIN_PACKAGE_INCLUDE_DESTINATION}
#   FILES_MATCHING PATTERN "*.h"
#   PATTERN ".svn" EXCLUDE
# )

## Mark other files for installation (e.g. launch and bag files, etc.)
# install(FILES
#   # myfile1
#   # myfile2
#   DESTINATION ${CATKIN_PACKAGE_SHARE_DESTINATION}
# )

#############
## Testing ##
#############

## Add gtest based cpp test target and link libraries
# catkin_add_gtest(${PROJECT_NAME}-test test/test_raven_2.cpp)
# if(TARGET ${PROJECT_NAME}-test)
#   target_link_libraries(${PROJECT_NAME}-test ${PROJECT_NAME})
# endif()

## Add folders to be run by python nosetests
# catkin_add_nosetests(test)
