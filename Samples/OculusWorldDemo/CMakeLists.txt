project(OculusWorldDemo)

set(EXTRA_LIBS 
	OculusVR
	CommonSrc
	TinyXML2
)

set(SOURCE_FILES 
    OculusWorldDemo.cpp
    Player.cpp
)

file(GLOB_RECURSE ASSET_FILES Assets/Tuscany/*)

if (WIN32)

    add_executable(OculusWorldDemo WIN32 ${SOURCE_FILES})

	add_custom_command(TARGET OculusWorldDemo POST_BUILD
		COMMAND ${CMAKE_COMMAND} -E copy_directory
        ${CMAKE_CURRENT_SOURCE_DIR}/Assets  ${CMAKE_CURRENT_BINARY_DIR}/Assets)

elseif (APPLE)

    list(APPEND SOURCE_FILES ${ASSET_FILES})

    set_source_files_properties(${ASSET_FILES} PROPERTIES MACOSX_PACKAGE_LOCATION Resources/Assets/Tuscany)

    add_executable(OculusWorldDemo MACOSX_BUNDLE ${SOURCE_FILES})

else()

    add_executable(OculusWorldDemo ${SOURCE_FILES})

	add_custom_command(TARGET OculusWorldDemo POST_BUILD
		COMMAND ${CMAKE_COMMAND} -E copy_directory
        ${CMAKE_CURRENT_SOURCE_DIR}/Assets  ${CMAKE_CURRENT_BINARY_DIR}/Assets)

endif()

target_link_libraries(OculusWorldDemo ${EXTRA_LIBS})
