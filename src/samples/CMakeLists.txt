project(SCT_SAMPLES)

MACRO(get_subdirectories result curdir)
  FILE(GLOB children RELATIVE ${curdir} ${curdir}/*)
  SET(dirlist "")
  FOREACH(child ${children})
    IF(IS_DIRECTORY ${curdir}/${child})
      LIST(APPEND dirlist ${child})
    ENDIF()
  ENDFOREACH()
  SET(${result} ${dirlist})
ENDMACRO()

# Enumerate all subdirs (http://stackoverflow.com/questions/7787823/cmake-how-to-get-the-name-of-all-subdirectories-of-a-directory)
get_subdirectories(DIRS_IN_SRC_SAMPLES_DIR "${CMAKE_SOURCE_DIR}/src/samples")

foreach(dir ${DIRS_IN_SRC_SAMPLES_DIR})
	# Set a VAR to allow enabling/disabling each project
	SET(VAR_NAME "SAMPLES_BUILD_${dir}")
	SET(${VAR_NAME} ON CACHE BOOL "Build the lib ${dir}")
	MARK_AS_ADVANCED(${VAR_NAME})

	# Add subdirectory for the project
	if(${VAR_NAME})
		add_subdirectory(${dir})
	endif(${VAR_NAME})
endforeach(dir)
