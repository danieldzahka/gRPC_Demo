include(FetchContent)
FetchContent_Declare(
        gRPC
        GIT_REPOSITORY https://github.com/grpc/grpc
)
set(FETCHCONTENT_QUIET OFF)
FetchContent_MakeAvailable(gRPC)

set(_PROTOBUF_LIBPROTOBUF libprotobuf)
set(_REFLECTION grpc++_reflection)
set(_PROTOBUF_PROTOC $<TARGET_FILE:protoc>)
set(_GRPC_GRPCPP grpc++)
set(_GRPC_CPP_PLUGIN_EXECUTABLE $<TARGET_FILE:grpc_cpp_plugin>)

cmake_print_properties(
        TARGETS protoc
        PROPERTIES TARGET_FILE
)

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

