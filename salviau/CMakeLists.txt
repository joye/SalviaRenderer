SALVIA_CHECK_BUILD_WITH_UNICODE()

INCLUDE_DIRECTORIES(
	${SALVIA_HOME_DIR}
	${SALVIA_WTL_INCLUDE_DIR}
	${SALVIA_BOOST_INCLUDE_DIR}
)

LINK_DIRECTORIES(
	${SALVIA_BOOST_LIB_DIR}
	${SALVIA_FREETYPE_LIB_DIR}
	${SALVIA_FREEIMAGE_LIB_DIR}
)

set( APP_COMMON_HEADERS
	${SALVIA_HOME_DIR}/salviau/include/common/gui.h
	${SALVIA_HOME_DIR}/salviau/include/common/benchmark.h
	${SALVIA_HOME_DIR}/salviau/include/common/window.h
	${SALVIA_HOME_DIR}/salviau/include/common/timer.h
	${SALVIA_HOME_DIR}/salviau/include/common/sample_app.h
	${SALVIA_HOME_DIR}/salviau/include/common/path.h
)

set( APP_WIN_HEADERS
	${SALVIA_HOME_DIR}/salviau/include/win/win_gui.h
)

set( APP_WIN_SOURCES
	${SALVIA_HOME_DIR}/salviau/src/win/win_gui.cpp
)

set( APP_WIN_IMPLS
	${SALVIA_HOME_DIR}/salviau/src/win/targetver.h
	${SALVIA_HOME_DIR}/salviau/src/win/resource.h
	${SALVIA_HOME_DIR}/salviau/src/win/salvia_win_app.rc
)

set( APP_COMMON_SOURCES
	${SALVIA_HOME_DIR}/salviau/src/common/timer.cpp
	${SALVIA_HOME_DIR}/salviau/src/common/sample_app.cpp
	${SALVIA_HOME_DIR}/salviau/src/common/path.cpp
)

SOURCE_GROUP( "Header Files\\Common"	FILES ${APP_COMMON_HEADERS} )
SOURCE_GROUP( "Source Files\\Common"	FILES ${APP_COMMON_SOURCES} )

SOURCE_GROUP( "Header Files\\Win"					FILES ${APP_WIN_HEADERS} )
SOURCE_GROUP( "Source Files\\Win\\Sources"			FILES ${APP_WIN_SOURCES} )
SOURCE_GROUP( "Source Files\\Win\\Implementations"	FILES ${APP_WIN_IMPLS} )

if(MSVC)
ADD_LIBRARY( salviau SHARED
	${APP_COMMON_HEADERS}
	${APP_COMMON_SOURCES}

	${APP_WIN_HEADERS}
	${APP_WIN_SOURCES}
	${APP_WIN_IMPLS}
)
else(MSVC)
ADD_LIBRARY( salviau SHARED
	${APP_COMMON_HEADERS}
	${APP_COMMON_SOURCES}
)
endif(MSVC)

TARGET_LINK_LIBRARIES( salviau salviax EFLIB ${SALVIA_BOOST_LIBS}) 
SET_TARGET_PROPERTIES( salviau PROPERTIES FOLDER "Samples" )

SALVIA_CONFIG_OUTPUT_PATHS(salviau)
