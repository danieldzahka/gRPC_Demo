# Proto file
set(demo_proto "demo.proto")

# Generated sources
set(demo_proto_srcs "${CMAKE_CURRENT_BINARY_DIR}/demo.pb.cc")
set(demo_proto_hdrs "${CMAKE_CURRENT_BINARY_DIR}/demo.pb.h")
set(demo_grpc_srcs "${CMAKE_CURRENT_BINARY_DIR}/demo.grpc.pb.cc")
set(demo_grpc_hdrs "${CMAKE_CURRENT_BINARY_DIR}/demo.grpc.pb.h")
add_custom_command(
        OUTPUT "${demo_proto_srcs}" "${demo_proto_hdrs}" "${demo_grpc_srcs}" "${demo_grpc_hdrs}"
        COMMAND protoc
        ARGS --grpc_out "${CMAKE_CURRENT_BINARY_DIR}"
        --cpp_out "${CMAKE_CURRENT_BINARY_DIR}"
        -I "${CMAKE_CURRENT_SOURCE_DIR}"
        --plugin=protoc-gen-grpc="${_GRPC_CPP_PLUGIN_EXECUTABLE}"
        "${demo_proto}"
        DEPENDS protoc grpc_cpp_plugin "${demo_proto}"
)

add_library(demo_grpc_proto
        ${demo_grpc_srcs}
        ${demo_grpc_hdrs}
        ${demo_proto_srcs}
        ${demo_proto_hdrs})

target_link_libraries(demo_grpc_proto
        PUBLIC
        grpc++_reflection
        grpc++
        libprotobuf
        )

target_include_directories(demo_grpc_proto
        PUBLIC
        ${CMAKE_CURRENT_BINARY_DIR})