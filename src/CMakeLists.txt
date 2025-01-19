# Generating the library x11vnc
set(project "x11vnc")

set(${project}, "")
list(APPEND ${project}_SOURCES
    ${CMAKE_CURRENT_SOURCE_DIR}/8to24.c
    ${CMAKE_CURRENT_SOURCE_DIR}/8to24.h
    ${CMAKE_CURRENT_SOURCE_DIR}/allowed_input_t.h
    ${CMAKE_CURRENT_SOURCE_DIR}/appshare.c
    ${CMAKE_CURRENT_SOURCE_DIR}/avahi.c
    ${CMAKE_CURRENT_SOURCE_DIR}/avahi.h
    ${CMAKE_CURRENT_SOURCE_DIR}/blackout_t.h
    ${CMAKE_CURRENT_SOURCE_DIR}/cleanup.c
    ${CMAKE_CURRENT_SOURCE_DIR}/cleanup.h
    ${CMAKE_CURRENT_SOURCE_DIR}/connections.c
    ${CMAKE_CURRENT_SOURCE_DIR}/connections.h
    ${CMAKE_CURRENT_SOURCE_DIR}/cursor.c
    ${CMAKE_CURRENT_SOURCE_DIR}/cursor.h
    ${CMAKE_CURRENT_SOURCE_DIR}/default8x16.h
    ${CMAKE_CURRENT_SOURCE_DIR}/enc.h
    ${CMAKE_CURRENT_SOURCE_DIR}/gui.c
    ${CMAKE_CURRENT_SOURCE_DIR}/gui.h
    ${CMAKE_CURRENT_SOURCE_DIR}/help.c
    ${CMAKE_CURRENT_SOURCE_DIR}/help.h
    ${CMAKE_CURRENT_SOURCE_DIR}/inet.c
    ${CMAKE_CURRENT_SOURCE_DIR}/inet.h
    ${CMAKE_CURRENT_SOURCE_DIR}/keyboard.c
    ${CMAKE_CURRENT_SOURCE_DIR}/keyboard.h
    ${CMAKE_CURRENT_SOURCE_DIR}/linuxfb.c
    ${CMAKE_CURRENT_SOURCE_DIR}/linuxfb.h
    ${CMAKE_CURRENT_SOURCE_DIR}/macosx.c
    ${CMAKE_CURRENT_SOURCE_DIR}/macosx.h
    ${CMAKE_CURRENT_SOURCE_DIR}/macosxCG.c
    ${CMAKE_CURRENT_SOURCE_DIR}/macosxCG.h
    ${CMAKE_CURRENT_SOURCE_DIR}/macosxCGP.c
    ${CMAKE_CURRENT_SOURCE_DIR}/macosxCGP.h
    ${CMAKE_CURRENT_SOURCE_DIR}/macosxCGS.c
    ${CMAKE_CURRENT_SOURCE_DIR}/macosxCGS.h
    ${CMAKE_CURRENT_SOURCE_DIR}/macosx_opengl.c
    ${CMAKE_CURRENT_SOURCE_DIR}/macosx_opengl.h
    ${CMAKE_CURRENT_SOURCE_DIR}/nox11.h
    ${CMAKE_CURRENT_SOURCE_DIR}/nox11_funcs.h
    ${CMAKE_CURRENT_SOURCE_DIR}/options.c
    ${CMAKE_CURRENT_SOURCE_DIR}/options.h
    ${CMAKE_CURRENT_SOURCE_DIR}/params.h
    ${CMAKE_CURRENT_SOURCE_DIR}/pm.c
    ${CMAKE_CURRENT_SOURCE_DIR}/pm.h
    ${CMAKE_CURRENT_SOURCE_DIR}/pointer.c
    ${CMAKE_CURRENT_SOURCE_DIR}/pointer.h
    ${CMAKE_CURRENT_SOURCE_DIR}/rates.c
    ${CMAKE_CURRENT_SOURCE_DIR}/rates.h
    ${CMAKE_CURRENT_SOURCE_DIR}/remote.c
    ${CMAKE_CURRENT_SOURCE_DIR}/remote.h
    ${CMAKE_CURRENT_SOURCE_DIR}/scan.c
    ${CMAKE_CURRENT_SOURCE_DIR}/scan.h
    ${CMAKE_CURRENT_SOURCE_DIR}/screen.c
    ${CMAKE_CURRENT_SOURCE_DIR}/screen.h
    ${CMAKE_CURRENT_SOURCE_DIR}/scrollevent_t.h
    ${CMAKE_CURRENT_SOURCE_DIR}/selection.c
    ${CMAKE_CURRENT_SOURCE_DIR}/selection.h
    ${CMAKE_CURRENT_SOURCE_DIR}/solid.c
    ${CMAKE_CURRENT_SOURCE_DIR}/solid.h
    ${CMAKE_CURRENT_SOURCE_DIR}/sslcmds.c
    ${CMAKE_CURRENT_SOURCE_DIR}/sslcmds.h
    ${CMAKE_CURRENT_SOURCE_DIR}/sslhelper.c
    ${CMAKE_CURRENT_SOURCE_DIR}/sslhelper.h
    ${CMAKE_CURRENT_SOURCE_DIR}/ssltools.h
    ${CMAKE_CURRENT_SOURCE_DIR}/tkx11vnc.h
    ${CMAKE_CURRENT_SOURCE_DIR}/uinput.c
    ${CMAKE_CURRENT_SOURCE_DIR}/uinput.h
    ${CMAKE_CURRENT_SOURCE_DIR}/unixpw.c
    ${CMAKE_CURRENT_SOURCE_DIR}/unixpw.h
    ${CMAKE_CURRENT_SOURCE_DIR}/user.c
    ${CMAKE_CURRENT_SOURCE_DIR}/user.h
    ${CMAKE_CURRENT_SOURCE_DIR}/userinput.c
    ${CMAKE_CURRENT_SOURCE_DIR}/userinput.h
    ${CMAKE_CURRENT_SOURCE_DIR}/util.c
    ${CMAKE_CURRENT_SOURCE_DIR}/util.h
    ${CMAKE_CURRENT_SOURCE_DIR}/v4l.c
    ${CMAKE_CURRENT_SOURCE_DIR}/v4l.h
    ${CMAKE_CURRENT_SOURCE_DIR}/win_utils.c
    ${CMAKE_CURRENT_SOURCE_DIR}/win_utils.h
    ${CMAKE_CURRENT_SOURCE_DIR}/winattr_t.h
    ${CMAKE_CURRENT_SOURCE_DIR}/x11vnc.c
    ${CMAKE_CURRENT_SOURCE_DIR}/x11vnc.h
    ${CMAKE_CURRENT_SOURCE_DIR}/x11vnc_defs.c
    ${CMAKE_CURRENT_SOURCE_DIR}/xdamage.c
    ${CMAKE_CURRENT_SOURCE_DIR}/xdamage.h
    ${CMAKE_CURRENT_SOURCE_DIR}/xevents.c
    ${CMAKE_CURRENT_SOURCE_DIR}/xevents.h
    ${CMAKE_CURRENT_SOURCE_DIR}/xi2_devices.c
    ${CMAKE_CURRENT_SOURCE_DIR}/xi2_devices.h
    ${CMAKE_CURRENT_SOURCE_DIR}/xinerama.c
    ${CMAKE_CURRENT_SOURCE_DIR}/xinerama.h
    ${CMAKE_CURRENT_SOURCE_DIR}/xkb_bell.c
    ${CMAKE_CURRENT_SOURCE_DIR}/xkb_bell.h
    ${CMAKE_CURRENT_SOURCE_DIR}/xrandr.c
    ${CMAKE_CURRENT_SOURCE_DIR}/xrandr.h
    ${CMAKE_CURRENT_SOURCE_DIR}/xrecord.c
    ${CMAKE_CURRENT_SOURCE_DIR}/xrecord.h
    ${CMAKE_CURRENT_SOURCE_DIR}/xwrappers.c
    ${CMAKE_CURRENT_SOURCE_DIR}/xwrappers.h
)

add_executable(x11vnc ${${project}_SOURCES} )
#set_target_properties( x11vnc
#    PROPERTIES COMPILE_FLAGS "-ObjC " # wat?
#)

target_link_libraries( x11vnc
	PRIVATE
	vncserver
	# $ grep -i vncserver config.log
	# configure:7443: checking for libvncserver >= 0.9.8
	# configure:7450: $PKG_CONFIG --exists --print-errors "libvncserver >= 0.9.8"
	# configure:7467: $PKG_CONFIG --exists --print-errors "libvncserver >= 0.9.8"
	# ac_cv_env_LIBVNCSERVER_CFLAGS_set=
	# ac_cv_env_LIBVNCSERVER_CFLAGS_value=
	# ac_cv_env_LIBVNCSERVER_LIBS_set=
	# ac_cv_env_LIBVNCSERVER_LIBS_value=
	# pkg_cv_LIBVNCSERVER_CFLAGS=
	# pkg_cv_LIBVNCSERVER_LIBS='-lvncserver '
	# LIBVNCSERVER_CFLAGS=''
	# LIBVNCSERVER_LIBS='-lvncserver '

	vncclient
	ssl
	drm
	crypt
	# they test no_x - if yes, #define X_DISPLAY_MISSING 1
	# if no (i.e. X is there?)
	# test -n "$x_includes" then X_CFLAGS="$X_CFLAGS -I$x_includes"
	# test -n "$x_libraries"; then X_LIBS="$X_LIBS -L$x_libraries"
	# i.e. these are user inputs?
	X11
	# there is also a user variable with_avahi?
	# which must contain the directory path to avahi:
	# AVAHI_CFLAGS="-I$with_avahi/include"
	# AVAHI_LIBS="-L$with_avahi/lib -lavahi-common -lavahi-client"
	# in my log:
	# $ grep -i avahi config.log 
	# AVAHI_CFLAGS=''
	# AVAHI_LIBS=''
	# also:
	#$ grep -i cairo config.log
	# CAIRO_CFLAGS=''
	# CAIRO_LIBS=''
	# HAVE_CAIRO_FALSE=''
	# HAVE_CAIRO_TRUE='#'
	# $ grep -i cygipc config.log
	# configure:9288: checking for shmget in -lcygipc
	# configure:9311: gcc -o conftest -g -O2  -I/usr/include/drm/  conftest.c -lcygipc   >&5
	# /usr/bin/ld: cannot find -lcygipc: No such file or directory
	# ac_cv_lib_cygipc_shmget=no
	# CYGIPC_FALSE=''
	# CYGIPC_TRUE='#'
)

# does not work???
target_include_directories( x11vnc
	PUBLIC
	${CMAKE_CURRENT_SOURCE_DIR}/
	# it looks like the target does not grab the project-wide include_directories()?
	${CMAKE_SOURCE_DIR}/
	"/usr/include/libdrm/"
)

#include_directories(
#	${CMAKE_CURRENT_SOURCE_DIR}/
#	"/usr/include/libdrm/"
#)

#target_link_libraries( x11vnc
#    @LIBVNCSERVER_LIBS@
#    @LIBVNCCLIENT_LIBS@
#    @WSOCKLIB@  # defined for some -lws2_32 $MINGW?
#    #it is a free and open source SW to develop GUI on Windows
#    "-lssl
#    crypto""-lssl"
#    "-ldrm"
#    "-lcrypt"
#    "$X_LIBS
#    $X_PRELIBS
#    X11
#    $X_EXTRA_LIBS"
#    lib
#    avahi-common
#    avahi-client"`pkg-config
#    --libs
#    avahi-client`
##    @XI2_LIBS@ # <-- FIX THIS
#    lib
#    cairo"`pkg-config
#    --libs
#    cairo`
#    cygipc
#)

