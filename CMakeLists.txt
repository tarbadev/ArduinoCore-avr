project(ArduinoCore
    VERSION 0.0.1
    DESCRIPTION "ArduinoCore"
    LANGUAGES CXX C)

file(GLOB HEADER_CORE_LIST CONFIGURE_DEPENDS "${SmartHome_SOURCE_DIR}/extern/ArduinoCore-avr/cores/arduino/*.h")
file(GLOB HEADER_VARIANT_LIST CONFIGURE_DEPENDS "${SmartHome_SOURCE_DIR}/extern/ArduinoCore-avr/variants/standard/*.h")

set(HEADER_LIST ${HEADER_CORE_LIST} ${HEADER_VARIANT_LIST})

list(APPEND arduino_core_include_path "${CMAKE_CURRENT_LIST_DIR}/cores/arduino" "${CMAKE_CURRENT_LIST_DIR}/variants/standard")

source_group(
    TREE "${CMAKE_CURRENT_LIST_DIR}/cores/arduino"
    PREFIX "Header Files"
    FILES ${HEADER_CORE_LIST})
source_group(
    TREE "${CMAKE_CURRENT_LIST_DIR}/variants/standard"
    PREFIX "Header Files"
    FILES ${HEADER_VARIANT_LIST})

if (${CMAKE_SYSTEM_NAME} MATCHES "Arduino")
  set(SOURCES
      ${CMAKE_CURRENT_LIST_DIR}/cores/arduino/abi.cpp
      ${CMAKE_CURRENT_LIST_DIR}/cores/arduino/CDC.cpp
      ${CMAKE_CURRENT_LIST_DIR}/cores/arduino/HardwareSerial.cpp
      ${CMAKE_CURRENT_LIST_DIR}/cores/arduino/HardwareSerial0.cpp
      ${CMAKE_CURRENT_LIST_DIR}/cores/arduino/HardwareSerial1.cpp
      ${CMAKE_CURRENT_LIST_DIR}/cores/arduino/HardwareSerial2.cpp
      ${CMAKE_CURRENT_LIST_DIR}/cores/arduino/HardwareSerial3.cpp
      ${CMAKE_CURRENT_LIST_DIR}/cores/arduino/IPAddress.cpp
      ${CMAKE_CURRENT_LIST_DIR}/cores/arduino/PluggableUSB.cpp
      ${CMAKE_CURRENT_LIST_DIR}/cores/arduino/Print.cpp
      ${CMAKE_CURRENT_LIST_DIR}/cores/arduino/Stream.cpp
      ${CMAKE_CURRENT_LIST_DIR}/cores/arduino/Tone.cpp
      ${CMAKE_CURRENT_LIST_DIR}/cores/arduino/USBCore.cpp
      ${CMAKE_CURRENT_LIST_DIR}/cores/arduino/WMath.cpp
      ${CMAKE_CURRENT_LIST_DIR}/cores/arduino/WString.cpp
      ${CMAKE_CURRENT_LIST_DIR}/cores/arduino/main.cpp
      ${CMAKE_CURRENT_LIST_DIR}/cores/arduino/new.cpp
      ${CMAKE_CURRENT_LIST_DIR}/cores/arduino/WInterrupts.c
      ${CMAKE_CURRENT_LIST_DIR}/cores/arduino/wiring.c
      ${CMAKE_CURRENT_LIST_DIR}/cores/arduino/wiring_analog.c
      ${CMAKE_CURRENT_LIST_DIR}/cores/arduino/wiring_digital.c
      ${CMAKE_CURRENT_LIST_DIR}/cores/arduino/wiring_pulse.c
      ${CMAKE_CURRENT_LIST_DIR}/cores/arduino/wiring_shift.c)

  add_library(arduino_core_lib STATIC ${SOURCES} ${HEADER_LIST})

  target_include_directories(arduino_core_lib PUBLIC ${arduino_core_include_path})
endif ()