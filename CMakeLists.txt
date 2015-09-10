cmake_minimum_required(VERSION 2.8.3)
project(raven_2)

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

add_message_files(
  FILES
  raven_automove.msg
  raven_state.msg
)

generate_messages(
  DEPENDENCIES
  std_msgs
  geometry_msgs
)

 generate_dynamic_reconfigure_options(
   cfg/MyStuff.cfg
 )

catkin_package()

include_directories(include ${catkin_INCLUDE_DIRS})

add_executable(r2_control
src/dof.cpp
src/fwd_cable_coupling.cpp
src/fwd_kinematics.cpp
src/r2_kinematics.cpp
src/get_USB_packet.cpp
src/globals.cpp
src/grav_comp.cpp
src/hmatrix.cpp
src/init.cpp
src/inv_cable_coupling.cpp
src/local_io.cpp
src/log.cpp
src/mapping.cpp
src/motor.cpp
src/network_layer.cpp
src/overdrive_detect.cpp
src/parallel.cpp
src/pid_control.cpp
src/put_USB_packet.cpp
src/rt_process_preempt.cpp
src/rt_raven.cpp
src/state_estimate.cpp
src/state_machine.cpp
src/homing.cpp
src/trajectory.cpp
src/console_process.cpp
src/t_to_DAC_val.cpp
src/update_atmel_io.cpp
src/update_device_state.cpp
src/USB_init.cpp
src/utils.cpp
src/reconfigure.cpp
src/tools.cpp
)

add_dependencies(r2_control ${catkin_EXPORTED_TARGETS})

target_link_libraries(r2_control
  ${catkin_LIBRARIES}
)

