cmake_minimum_required(VERSION 3.1...3.25)
project(
    shrimp_gpu
	VERSION 0.1.0
	LANGUAGES CXX C
)

include(utils.cmake)

add_subdirectory(glfw)
add_subdirectory(webgpu)
add_subdirectory(glfw3webgpu)

add_executable(app
	main.cc
	webgputils.h
	webgputils.cc
)

target_link_libraries(app PRIVATE glfw webgpu glfw3webgpu)

set_target_properties(app PROPERTIES
	CXX_STANDARD 17
	VS_DEBUGGER_ENVIRONMENT "DAWN_DEBUG_BREAK_ON_ERROR=1"
)
target_treat_all_warnings_as_errors(app)
target_copy_webgpu_binaries(app)
