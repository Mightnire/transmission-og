BUILT_SOURCES =
CLEANFILES =

AM_CPPFLAGS = -I@top_srcdir@

AM_CFLAGS = \
    @LIBEVENT_CFLAGS@ \
    @LIBCURL_CFLAGS@ \
    @ZLIB_CFLAGS@ \
    @PTHREAD_CFLAGS@

bin_PROGRAMS = \
    transmission-create \
    transmission-edit \
    transmission-remote \
    transmission-show

transmission_create_SOURCES = create.c
nodist_EXTRA_transmission_create_SOURCES = dummy.cxx # force C++ linking
transmission_edit_SOURCES = edit.c
nodist_EXTRA_transmission_edit_SOURCES = dummy.cxx # force C++ linking
transmission_remote_SOURCES = remote.c
nodist_EXTRA_transmission_remote_SOURCES = dummy.cxx # force C++ linking
transmission_show_SOURCES = show.c
nodist_EXTRA_transmission_show_SOURCES = dummy.cxx # force C++ linking

noinst_HEADERS = \
    units.h \
    ../libtransmission/version.h

dist_man_MANS = \
    transmission-create.1 \
    transmission-edit.1 \
    transmission-remote.1 \
    transmission-show.1

common_ldadd = \
    $(top_builddir)/libtransmission/libtransmission.la \
    @LIBEVENT_LIBS@
transmission_create_LDADD = $(common_ldadd)
transmission_edit_LDADD = $(common_ldadd)
transmission_remote_LDADD = $(common_ldadd)
transmission_show_LDADD = $(common_ldadd)

if WIN32
transmission-create.rc: ../transmission.rc.in
	TR_FILE_DESCRIPTION="Transmission OG Utility ('create')"; \
	TR_INTERNAL_NAME="$(PACKAGE_NAME)-create"; \
	TR_ORIGINAL_FILENAME="$(PACKAGE_NAME)-create.exe"; \
	HAVE_ICON=0; \
	sed \
	-e "s/%TR_FILE_DESCRIPTION%/$${TR_FILE_DESCRIPTION}/" \
	-e "s/%TR_INTERNAL_NAME%/$${TR_INTERNAL_NAME}/" \
	-e "s/%TR_ORIGINAL_FILENAME%/$${TR_ORIGINAL_FILENAME}/" \
	-e "s/%HAVE_ICON%/$${HAVE_ICON}/" \
	$< > $@

transmission-create.res: transmission-create.rc ../libtransmission/version.h
	$(WINDRES) -J rc -I $(top_srcdir) -i $< -O coff -o $@

BUILT_SOURCES += transmission-create.res
CLEANFILES += transmission-create.rc transmission-create.res
transmission_create_LDADD += transmission-create.res

transmission-edit.rc: ../transmission.rc.in
	TR_FILE_DESCRIPTION="Transmission OG Utility ('edit')"; \
	TR_INTERNAL_NAME="$(PACKAGE_NAME)-edit"; \
	TR_ORIGINAL_FILENAME="$(PACKAGE_NAME)-edit.exe"; \
	HAVE_ICON=0; \
	sed \
	-e "s/%TR_FILE_DESCRIPTION%/$${TR_FILE_DESCRIPTION}/" \
	-e "s/%TR_INTERNAL_NAME%/$${TR_INTERNAL_NAME}/" \
	-e "s/%TR_ORIGINAL_FILENAME%/$${TR_ORIGINAL_FILENAME}/" \
	-e "s/%HAVE_ICON%/$${HAVE_ICON}/" \
	$< > $@

transmission-edit.res: transmission-edit.rc ../libtransmission/version.h
	$(WINDRES) -J rc -I $(top_srcdir) -i $< -O coff -o $@

BUILT_SOURCES += transmission-edit.res
CLEANFILES += transmission-edit.rc transmission-edit.res
transmission_edit_LDADD += transmission-edit.res

transmission-remote.rc: ../transmission.rc.in
	TR_FILE_DESCRIPTION="Transmission OG Utility ('remote')"; \
	TR_INTERNAL_NAME="$(PACKAGE_NAME)-remote"; \
	TR_ORIGINAL_FILENAME="$(PACKAGE_NAME)-remote.exe"; \
	HAVE_ICON=0; \
	sed \
	-e "s/%TR_FILE_DESCRIPTION%/$${TR_FILE_DESCRIPTION}/" \
	-e "s/%TR_INTERNAL_NAME%/$${TR_INTERNAL_NAME}/" \
	-e "s/%TR_ORIGINAL_FILENAME%/$${TR_ORIGINAL_FILENAME}/" \
	-e "s/%HAVE_ICON%/$${HAVE_ICON}/" \
	$< > $@

transmission-remote.res: transmission-remote.rc ../libtransmission/version.h
	$(WINDRES) -J rc -I $(top_srcdir) -i $< -O coff -o $@

BUILT_SOURCES += transmission-remote.res
CLEANFILES += transmission-remote.rc transmission-remote.res
transmission_remote_LDADD += transmission-remote.res

transmission-show.rc: ../transmission.rc.in
	TR_FILE_DESCRIPTION="Transmission OG Utility ('show')"; \
	TR_INTERNAL_NAME="$(PACKAGE_NAME)-show"; \
	TR_ORIGINAL_FILENAME="$(PACKAGE_NAME)-show.exe"; \
	HAVE_ICON=0; \
	sed \
	-e "s/%TR_FILE_DESCRIPTION%/$${TR_FILE_DESCRIPTION}/" \
	-e "s/%TR_INTERNAL_NAME%/$${TR_INTERNAL_NAME}/" \
	-e "s/%TR_ORIGINAL_FILENAME%/$${TR_ORIGINAL_FILENAME}/" \
	-e "s/%HAVE_ICON%/$${HAVE_ICON}/" \
	$< > $@

transmission-show.res: transmission-show.rc ../libtransmission/version.h
	$(WINDRES) -J rc -I $(top_srcdir) -i $< -O coff -o $@

BUILT_SOURCES += transmission-show.res
CLEANFILES += transmission-show.rc transmission-show.res
transmission_show_LDADD += transmission-show.res
endif #WIN32
