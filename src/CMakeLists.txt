set(MOONSRC
	buggy.c
	cursor.c
	date.c
	error.c
	game.c
	ground.c
	highscore.c
	hpath.c
	keyboard.c
	laser.c
	level.c
	main.c
	meteor.c
	mode.c
	pager.c
	persona.c
	queue.c
	random.c
	realname.c
	signal.c
	terminal.c
	title.c
	vclock.c
	xmalloc.c
	xstrdup.c
)

set(SHAREDSCOREDIR "/tmp" CACHE PATH "The shared score diretory")

set(GENINCDIR ${CMAKE_CURRENT_BINARY_DIR}/include)
file(MAKE_DIRECTORY ${GENINCDIR})
execute_process(
	COMMAND
		sed -f text2c.sed COPYING
	WORKING_DIRECTORY
		${PROJECT_SOURCE_DIR}
	OUTPUT_FILE
		${GENINCDIR}/copying.h
)
execute_process(
	COMMAND
		sed -n -f img.sed car.img
	WORKING_DIRECTORY
		${PROJECT_SOURCE_DIR}
	OUTPUT_FILE
		${GENINCDIR}/buggy.h
)
include_directories(${GENINCDIR})

add_definitions(
	-DHAVE_ERRNO_H
	-DSCORE_DIR="${SHAREDSCOREDIR}"
	-DVERSION="2.0"
)

add_executable("moon-buggy" ${MOONSRC})

target_link_libraries("moon-buggy" ${LIBRARIES})
