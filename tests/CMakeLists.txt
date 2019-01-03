# --------------------------------------------------------------------------- #
# Author:       Joey Dumont                      <joey.dumont@gmail.com>      #
# Date created: 201-09- 04                                                    #
# Description:  CMake compilation instructions for the Zernike tests.         #
# ----------------------------------------------------------------------------#


# -- Dependency (Google Test)
find_package(GTest REQUIRED)
include_directories(${GTEST_INCLUDE_DIRS})
set(LIBS ${LIBS} ${GTEST_LIBRARIES})

find_package(armadillo)
include_directories(${armadillo_INCLUDE_DIR})

set(THREADS_PREFER_PTHREAD_FLAG ON)
find_package(Threads REQUIRED)

# -- Output tests in directory
add_executable("UnitTest-IndexConversion" "UnitTest-IndexConversion.cpp")
target_link_libraries("UnitTest-IndexConversion" ${PROJECT_NAME} ${LIBS})
target_link_libraries("UnitTest-IndexConversion" Threads::Threads)
add_test(NAME "UnitTest-IndexConversion" COMMAND "UnitTest-IndexConversion")

add_executable("UnitTest-ZernikePolynomials" "UnitTest-ZernikePolynomials.cpp")
target_link_libraries("UnitTest-ZernikePolynomials" ${PROJECT_NAME} ${LIBS} ${armadillo_LIBRARY})
target_link_libraries("UnitTest-ZernikePolynomials" Threads::Threads)
add_test(NAME "UnitTest-ZernikePolynomials" COMMAND "UnitTest-ZernikePolynomials")
