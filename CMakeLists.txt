cmake_minimum_required (VERSION 3.10.2)

##### PLUGIN NAME #####
set(pluginname gipEmptyPlugin)


##### PLUGIN PATHS #####
set(PLUGIN_DIR ${PLUGINS_DIR}/${pluginname})
set(PLUGIN_LIBS_DIR ${PLUGIN_DIR}/libs)
set(PLUGIN_PREBUILTS_DIR ${PLUGIN_DIR}/prebuilts)


##### PLUGIN SOURCES #####
list(APPEND PLUGIN_SRCS
			${PLUGIN_DIR}/src/gipEmptyPlugin.cpp
)


##### PLUGIN HEADERS #####
list(APPEND PLUGIN_INCLUDES
			${PLUGIN_DIR}/src
)
if(EXISTS "${PLUGIN_LIBS_DIR}/include")
	list(APPEND PLUGIN_INCLUDES "${PLUGIN_LIBS_DIR}/include")
endif()
if(EXISTS "${PLUGIN_PREBUILTS_DIR}/include")
	list(APPEND PLUGIN_INCLUDES "${PLUGIN_PREBUILTS_DIR}/include")
endif()


##### PLUGIN DEPENDENCY LOCATIONS & DLL COPYING (IF ANY) #####
if(WIN32)
	# Automatically copy all prebuilt runtime DLLs to application binary directory
	file(GLOB PLUGIN_DLLS
		"${PLUGIN_LIBS_DIR}/bin/*.dll"
		"${PLUGIN_PREBUILTS_DIR}/bin/*.dll"
	)
	if(PLUGIN_DLLS)
		file(COPY ${PLUGIN_DLLS} DESTINATION ${CMAKE_BINARY_DIR})
	endif()

	if(EXISTS "${PLUGIN_LIBS_DIR}/lib/win32")
		list(APPEND PLUGIN_LINKDIRS "${PLUGIN_LIBS_DIR}/lib/win32")
		list(APPEND PLUGIN_LIBDIRS "${PLUGIN_LIBS_DIR}/lib/win32")
	endif()
	if(EXISTS "${PLUGIN_LIBS_DIR}/bin")
		list(APPEND PLUGIN_LINKDIRS "${PLUGIN_LIBS_DIR}/bin")
	endif()

	if(EXISTS "${PLUGIN_PREBUILTS_DIR}/lib/win32")
		list(APPEND PLUGIN_LINKDIRS "${PLUGIN_PREBUILTS_DIR}/lib/win32")
		list(APPEND PLUGIN_LIBDIRS "${PLUGIN_PREBUILTS_DIR}/lib/win32")
	endif()
	if(EXISTS "${PLUGIN_PREBUILTS_DIR}/bin")
		list(APPEND PLUGIN_LINKDIRS "${PLUGIN_PREBUILTS_DIR}/bin")
	endif()
elseif(LINUX)
	# Linux libs & includes here
elseif(APPLE)
	# macOS / iOS libs & includes here
endif(WIN32)


##### PLUGIN DEPENDENCY LINKING (IF ANY) #####					
if(WIN32)
	list(APPEND PLUGIN_LINKLIBS
				# Add your library link names here (e.g. mylib, zlib)
	)
elseif(LINUX)
	list(APPEND PLUGIN_LINKLIBS
				# Add your Linux library link names here
	)
elseif(APPLE)
	list(APPEND PLUGIN_LINKLIBS
				# Add your macOS library link names here
	)
endif(WIN32)
