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

# Have the README.md in the install directory
install(FILES "README.md" DESTINATION ".")
install(FILES "CHANGELOG.md" DESTINATION ".")
install(FILES "LICENSE.md" DESTINATION ".")



include(CMakePackageConfigHelpers)

write_basic_package_version_file("${CMAKE_CURRENT_BINARY_DIR}/NostraSQLiteConfigVersion.cmake"
	VERSION "${NostraSQLite_VERSION}"
	COMPATIBILITY AnyNewerVersion)

export(EXPORT NostraSQLiteTargets
	FILE "${CMAKE_CURRENT_BINARY_DIR}/NostraSQLiteConfig.cmake"
	NAMESPACE Nostra::)

configure_file("cmake/NostraSQLiteConfig.cmake" "${CMAKE_CURRENT_BINARY_DIR}/NostraSQLiteConfig.cmake" COPYONLY)

set(CONFIG_PACKAGE_LOCATION "lib/cmake/NostraSQLite")

install(EXPORT NostraSQLiteTargets
	FILE
		NostraSQLiteConfig.cmake
	NAMESPACE
		Nostra::
	DESTINATION
		${CONFIG_PACKAGE_LOCATION})

install(
  FILES
    cmake/NostraSQLiteConfig.cmake
    "${CMAKE_CURRENT_BINARY_DIR}/NostraSQLiteConfig.cmake"
  DESTINATION
    ${CONFIG_PACKAGE_LOCATION}
  COMPONENT
    Develop
)


configure_file("cmake/CPackConfig.cmake" "cmake/CPackConfig.cmake" @ONLY)

include("${CMAKE_BINARY_DIR}/cmake/CPackConfig.cmake")

include(CPack)