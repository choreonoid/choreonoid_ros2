set(target CnoidROS2Plugin)

choreonoid_make_gettext_mo_files(${target} mofiles)

choreonoid_add_plugin(${target}
        ROS2Plugin.cpp
        WorldROS2Item.cpp
        BodyROS2Item.cpp
        deprecated/BodyPublisherItem.cpp
        ${mofiles}
  )

target_include_directories(${target} PRIVATE
  ${rclcpp_INCLUDE_DIRS}
  ${std_msgs_INCLUDE_DIRS}
  ${std_srvs_INCLUDE_DIRS}
  ${sensor_msgs_INCLUDE_DIRS}
  ${image_transport_INCLUDE_DIRS}
  )

target_link_libraries(${target} PRIVATE
  ${rclcpp_LIBRARIES}
  ${std_msgs_LIBRARIES}
  ${std_srvs_LIBRARIES}
  ${sensor_msgs_LIBRARIES}
  ${image_transport_LIBRARIES}
  Choreonoid::CnoidBodyPlugin
  )

if(CHOREONOID_ENABLE_PYTHON)
#  add_subdirectory(pybind11)
endif()

install(TARGETS ${target}
        LIBRARY DESTINATION lib/${PROJECT_NAME})
