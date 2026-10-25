BUILT_SOURCES =
CLEANFILES =
EXTRA_DIST = CMakeLists.txt

AM_CPPFLAGS = -I@top_srcdir@

AM_CFLAGS = \
    @LIBEVENT_CFLAGS@ \
    @LIBCURL_CFLAGS@ \
    @ZLIB_CFLAGS@ \
    @PTHREAD_CFLAGS@

bin_PROGRAMS = transmission-cli

dist_man_MANS = transmission-cli.1

transmission_cli_SOURCES = \
			      cli.c \
			      ../libtransmission/version.h
nodist_EXTRA_transmission_cli_SOURCES = dummy.cxx # force C++ linking

transmission_cli_LDADD = \
    $(top_builddir)/libtransmission/libtransmission.la \
    @LIBEVENT_LIBS@

if WIN32
transmission-cli.rc: ../transmission.rc.in
	TR_FILE_DESCRIPTION="Transmission OG Utility ('cli', obsolete)"; \
	TR_INTERNAL_NAME="$(PACKAGE_NAME)-cli"; \
	TR_ORIGINAL_FILENAME="$(PACKAGE_NAME)-cli.exe"; \
	HAVE_ICON=0; \
	sed \
	-e "s/%TR_FILE_DESCRIPTION%/$${TR_FILE_DESCRIPTION}/" \
	-e "s/%TR_INTERNAL_NAME%/$${TR_INTERNAL_NAME}/" \
	-e "s/%TR_ORIGINAL_FILENAME%/$${TR_ORIGINAL_FILENAME}/" \
	-e "s/%HAVE_ICON%/$${HAVE_ICON}/" \
	$< > $@

transmission-cli.res: transmission-cli.rc ../libtransmission/version.h
	$(WINDRES) -J rc -I $(top_srcdir) -i $< -O coff -o $@

BUILT_SOURCES += transmission-cli.res
CLEANFILES += transmission-cli.rc transmission-cli.res
transmission_cli_LDADD += transmission-cli.res
endif #WIN32
