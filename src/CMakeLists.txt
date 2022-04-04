#include(FetchContent)
#FetchContent_Declare(
#        gRPC
#        GIT_REPOSITORY https://github.com/grpc/grpc
#        GIT_TAG v1.28.0
#)
#set(FETCHCONTENT_QUIET OFF)
#FetchContent_MakeAvailable(gRPC)

add_executable(client client.cpp)
target_link_libraries(client
        PRIVATE
        project_options
        project_warnings)

add_executable(server server.cpp)
target_link_libraries(server
        PRIVATE
        project_options
        project_warnings)
