include(FlightGearComponent)

set(EVENT_INPUT_SOURCES
	FGLinuxEventInput.cxx
	FGMacOSXEventInput.cxx
	)

set(SOURCES
	FGButton.cxx
	FGCommonInput.cxx
	FGDeviceConfigurationMap.cxx
	FGEventInput.cxx
	FGJoystickInput.cxx
	FGKeyboardInput.cxx
	FGMouseInput.cxx
	input.cxx	
	)
	
if(EVENT_INPUT)
	list(APPEND SOURCES ${EVENT_INPUT_SOURCES})
endif()
	
set(FGJS_SOURCES
	fgjs.cxx
	jsinput.cxx
	jssuper.cxx
	)
	
add_executable(fgjs ${FGJS_SOURCES})

if(WIN32)
   set(SOCKETS_LIBRARY wsock32.lib)
endif(WIN32)

target_link_libraries(fgjs 
    ${SOCKETS_LIBRARY}
	${SIMGEAR_LIBRARIES}
	${PLIB_LIBRARIES}
	${ZLIB_LIBRARY})

add_executable(js_demo js_demo.cxx)

target_link_libraries(js_demo 
	${SIMGEAR_LIBRARIES}
	${PLIB_LIBRARIES}
	${ZLIB_LIBRARY})

flightgear_component(Input "${SOURCES}")

install(TARGETS fgjs js_demo RUNTIME DESTINATION bin)