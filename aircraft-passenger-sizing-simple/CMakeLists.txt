cmake_minimum_required(VERSION 3.27)
project(aircraft_passenger_sizing_simple)

set(CMAKE_CXX_STANDARD 17)
set(GUROBI_INCLUDE_DIRECTORY "/Library/gurobi1101/macos_universal2/include")
set(GUROBI_LIB_DIRECTORY "")

add_executable(aircraft_passenger_sizing_simple passenger-sizing-simple.cpp)
