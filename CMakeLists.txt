cmake_minimum_required(VERSION 3.5)
project(expressiongraph)

# Default to C++14
if(NOT CMAKE_CXX_STANDARD)
  set(CMAKE_CXX_STANDARD 14)
endif()

if(CMAKE_COMPILER_IS_GNUCXX OR CMAKE_CXX_COMPILER_ID MATCHES "Clang")
  add_compile_options(-Wall -Wextra -Wpedantic)
endif()

find_package(ament_cmake REQUIRED)

find_package(Eigen3 REQUIRED)
find_package(orocos_kdl REQUIRED)

add_library(${PROJECT_NAME} SHARED 
    src/expressiontree_expressions.cpp  
    src/expressiontree_motionprofiles.cpp    
    src/expressiontree_rotation.cpp  
    src/expressiontree_wrench.cpp
    src/expressiontree_chain.cpp   
    src/expressiontree_frame.cpp        
    src/expressiontree_twist.cpp     
    src/mptrap.cpp
    src/expressiontree_double.cpp  
    src/expressiontree_mimo.cpp         
    src/expressiontree_vector.cpp)

target_include_directories(${PROJECT_NAME} PRIVATE include)
ament_target_dependencies(${PROJECT_NAME} orocos_kdl)

install(
  DIRECTORY include/
  DESTINATION include
)

install(
  TARGETS
  ${PROJECT_NAME}
  RUNTIME DESTINATION bin
  ARCHIVE DESTINATION lib
  LIBRARY DESTINATION lib)

ament_export_include_directories(
  include)

ament_export_libraries(
  ${PROJECT_NAME})

ament_package()