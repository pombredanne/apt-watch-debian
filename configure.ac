dnl                                                -*- Autoconf -*-
dnl  Initial template generated by autoscan

AC_INIT
AC_CONFIG_SRCDIR([backend/apt-watch-slave.cc])
AM_INIT_AUTOMAKE(apt-watch, 0.4.0)
dnl AC_CONFIG_SRCDIR([apt-watch.cc])
dnl AM_CONFIG_HEADER([config.h])
AM_CONFIG_HEADER(config.h)

AM_MAINTAINER_MODE

AC_LANG([C++])

dnl  Checks for programs.
AC_PROG_CXX
AC_PROG_CC
AC_PROG_MAKE_SET
AC_PROG_RANLIB

dnl  Checks for libraries.

dnl  Checks for header files.
AC_HEADER_STDC
dnl AC_CHECK_HEADERS([stdlib.h string.h unistd.h])

dnl  Checks for typedefs, structures, and compiler characteristics.
dnl   2.5:
dnl AC_HEADER_STDBOOL

dnl  Checks for library functions.
dnl   2.5:
dnl AC_FUNC_FORK
dnl AC_FUNC_MALLOC
AC_TYPE_SIGNAL
dnl AC_CHECK_FUNCS([dup2 memset])

dnl  Gnome 2 tests.  Is this documented ANYWHERE??
dnl 
dnl  Scavenged from bubblemon

LIBPANEL_REQUIRED=3.0.0.0

PKG_CHECK_MODULES(GNOME_APPLETS,
		[libpanelapplet-4.0 >= $LIBPANEL_REQUIRED],
		build_gpanel=true,
		[AC_MSG_ERROR([libpanel-applet 4 required, not found.])] )

LIBPANEL_APPLET_DIR=`$PKG_CONFIG --variable=libpanel_applet_dir libpanelapplet-4.0`
AC_SUBST(LIBPANEL_APPLET_DIR)

AC_LANG_PUSH(C)
AC_LANG_POP(C)

AM_GCONF_SOURCE_2

CXXFLAGS="$CXXFLAGS -Wall"

AC_CHECK_HEADER(apt-pkg/init.h, , [AC_MSG_ERROR([Can't find the APT header files -- please install libapt-pkg-dev])])

AC_CHECK_LIB(apt-pkg, main, [AC_DEFINE(HAVE_LIBAPT_PKG, [], [Define to 1 if you have the apt-pkg library])], [AC_MSG_ERROR([Can't find the APT library -- please install libapt-pkg-dev])])

FAM_LDADD=""

AC_CHECK_HEADERS(fam.h)
AC_CHECK_LIB(fam, FAMOpen, [AC_DEFINE(HAVE_LIBFAM, [], [Define to 1 if you have the fam library])
			    FAM_LDADD="-lfam"])

dnl TODO: this is really optional if the suid helper can be disabled.
AC_CHECK_HEADER(security/pam_appl.h, , [AC_MSG_ERROR([Can't find the PAM header files -- please install libpam0g-dev])])
AC_CHECK_LIB(pam, main, [AC_DEFINE(HAVE_LIBPAM, [], [Define to 1 if you have the pam library])],
	    [AC_MSG_ERROR([Can't find the PAM library -- please install libpam0g-dev])])


dnl Allow the user to enable debugging
AC_ARG_ENABLE(debug,
	AS_HELP_STRING([--enable-debug], [Log debugging information to /tmp]),
	if test x$enableval = xyes
	then
	  [AC_DEFINE(DEBUG, 1, [Enable the logging of debugging information])]
	fi)

AC_SUBST(GNOME_INCLUDES, "$GNOME_APPLETS_CFLAGS")

AC_SUBST(GNOME_LDADD, "$GNOME_APPLETS_LIBS")

AC_SUBST(FAM_LDADD, "$FAM_LDADD")

FC_EXPAND_DIR(DATADIR, "$datadir")
AC_DEFINE_UNQUOTED(DATADIR, "$DATADIR", [The directory in which to place data files])

FC_EXPAND_DIR(LIBEXECDIR, "$libexecdir")
AC_DEFINE_UNQUOTED(LIBEXECDIR, "$LIBEXECDIR", [The directory in which to place private executables])

dnl AC_CONFIG_FILES([Makefile])
AC_CONFIG_FILES([Makefile backend/Makefile
		 common/Makefile ui-gnome/Makefile ui-gnome/pixmaps/Makefile])
AC_OUTPUT
