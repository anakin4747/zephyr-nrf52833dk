cmake_minimum_required(VERSION 3.20.0)

set(BOARD nrf52833dk/nrf52833)

find_package(Zephyr)
project(blinky)

target_sources(app PRIVATE src/main.c)
