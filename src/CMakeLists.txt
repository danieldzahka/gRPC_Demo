set(ABSL_PROPAGATE_CXX_STD ON)

include(FetchContent)
FetchContent_Declare(
        gRPC
        GIT_REPOSITORY https://github.com/grpc/grpc
        GIT_TAG        v1.45.0
)
set(FETCHCONTENT_QUIET OFF)
FetchContent_MakeAvailable(gRPC)

set(_GRPC_CPP_PLUGIN_EXECUTABLE $<TARGET_FILE:grpc_cpp_plugin>)

add_subdirectory(proto)

add_executable(client client.cpp)
target_link_libraries(client
        PRIVATE
        project_options
        project_warnings
        demo_grpc_proto
        )

add_executable(server server.cpp)
target_link_libraries(server
        PRIVATE
        project_options
        project_warnings
        demo_grpc_proto
        )
