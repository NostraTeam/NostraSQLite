cmake_minimum_required(VERSION 3.1 FATAL_ERROR)

project(NostraSQLite 
    VERSION 3.23.1
    DESCRIPTION "A Nostra-compatible SQLite version."
    LANGUAGES C)

add_library(SQLite SHARED "src/sqlite3.c")

#the sqlite3.h is contained within the sqlite3.c, therefore INTERFACE is enough
target_include_directories(SQLite 
    INTERFACE 
        "$<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include>"
        "$<INSTALL_INTERFACE:include>")

target_compile_definitions(SQLite 
    PRIVATE 
        NOU_SQLITE3_EXPORT
        NOU_SQLITE3_EXPORT_BUILD)

install(TARGETS SQLite EXPORT NostraSQLiteTargets
    RUNTIME  DESTINATION "bin"
    LIBRARY  DESTINATION "lib"
    ARCHIVE  DESTINATION "lib"
    INCLUDES DESTINATION "include")

install(DIRECTORY "include" 
    DESTINATION 
        "include" 
    COMPONENT 
        Develop)