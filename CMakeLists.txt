cmake_minimum_required(VERSION 3.0.0)
project(served)

find_package(CURL REQUIRED)
find_package(Threads)
find_package(Boost REQUIRED)

# Setting Output Directorys
set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/bin)
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/bin)
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/bin)

set(SRC_FILES 
    "methods_handler.cpp"
    "multiplexer.cpp"
    "parameters.cpp"
    "request_parser_impl.cpp"
    "request_parser.cpp"
    "request.cpp"
    "response.cpp"
    "status.cpp"
    "uri.cpp"

    "mux/regex_matcher.cpp"
    "mux/static_matcher.cpp"
    "mux/variable_matcher.cpp"

    "net/connection_manager.cpp"
    "net/connection.cpp"
    "net/server.cpp"

    "plugins/access_log.cpp"
)

include_directories(../ ${CURL_INCLUDE_DIRS} ${Boost_INCLUDE_DIRS})

add_library(served STATIC ${SRC_FILES})
target_link_libraries(served ${CMAKE_THREAD_LIBS_INIT} ${Boost_LIBRARIES} ${CURL_LIBRARIES})