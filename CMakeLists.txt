cmake_minimum_required(VERSION 2.8.3)
project(giskard_pr2)

find_package(catkin REQUIRED COMPONENTS
  giskard_ros
  iai_pr2_sim)

catkin_package()
