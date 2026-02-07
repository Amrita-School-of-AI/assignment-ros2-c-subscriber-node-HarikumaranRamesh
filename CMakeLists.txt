cmake_minimum_required(VERSION 3.8)
project(ros2_subscriber)

# Use modern C++
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

if(CMAKE_COMPILER_IS_GNUCXX OR CMAKE_CXX_COMPILER_ID MATCHES "Clang")
  add_compile_options(-Wall -Wextra -Wpedantic)
endif()

# Dependencies
find_package(ament_cmake REQUIRED)
find_package(rclcpp REQUIRED)
find_package(std_msgs REQUIRED)

# Executable
add_executable(subscriber_node src/subscriber_node.cpp)

# Link ROS2 libraries
ament_target_dependencies(subscriber_node
  rclcpp
  std_msgs
)

# Install node
install(TARGETS
  subscriber_node
  DESTINATION lib/${PROJECT_NAME}
)

# Testing & linting
if(BUILD_TESTING)
  find_package(ament_lint_auto REQUIRED)
  ament_lint_auto_find_test_dependencies()
endif()

ament_package()
