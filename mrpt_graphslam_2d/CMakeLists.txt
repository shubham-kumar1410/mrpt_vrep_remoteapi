PROJECT(mrpt_graphslam_2d)
set(PROJECT_TEST_NAME ${PROJECT_NAME}_test)

if (BUILD_TESTING)
	set(test_sources test/runTests.cpp )
	add_executable(${PROJECT_TEST_NAME} ${test_sources})
	target_link_libraries(${PROJECT_TEST_NAME}
	  gtest pthread )
  set_target_properties(${PROJECT_TEST_NAME} PROPERTIES
    RUNTIME_OUTPUT_DIRECTORY ${test_output_directory} )
  add_test(NAME ${PROJECT_TEST_NAME} COMMAND
    ${test_output_directory}/${PROJECT_TEST_NAME})
endif()

add_definitions (-DNON_MATLAB_PARSING)
add_definitions (-DMAX_EXT_API_CONNECTIONS=255)
add_executable(graphslamapi remoteApi/graphslam2d_remoteapi.cpp)
include_directories(include)
target_link_libraries(graphslamapi vrep_lib pthread rt conversion_lib)
