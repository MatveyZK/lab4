cmake_minimum_required(VERSION 3.11)

if(NOT DEFINED CI_PROJECT_VERSION)
 set(CI_PROJECT_VERSION "0.0.0")
endif()

project(lab6 VERSION ${CI_PROJECT_VERSION})

add_subdirectory(formatter_lib)
add_subdirectory(formatter_ex_lib)
add_subdirectory(solver_lib)
add_subdirectory(hello_world_application)
add_subdirectory(solver_application)

install(TARGETS equation RUNTIME DESTINATION bin)

set(CPACK_PACKAGE_NAME "solver")
set(CPACK_PACKAGE_VENDOR "Matvey.inc")
set(CPACK_PACKAGE_CONTACT ${GITHUB_EMAIL})
set(CPACK_PACKAGE_DESCRIPTION_SUMMARY "app for solving quadratic equations")

set(CPACK_DEBIAN_PACKAGE_MAINTAINER "Matvey")
set(CPACK_DEBIAN_PACKAGE_DEPENDS "libc (>= 2.43)")
set(CPACK_RPM_PACKAGE_REQUIRES "glibc >= 2.43")

include(CPack)
