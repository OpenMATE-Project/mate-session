bin_PROGRAMS = gnome-session
noinst_LTLIBRARIES = libgsmutil.la
noinst_PROGRAMS = 		\
	test-client-dbus	\
	test-inhibit

AM_CPPFLAGS =					\
	$(GNOME_SESSION_CFLAGS)			\
	$(DISABLE_DEPRECATED_CFLAGS)

AM_CFLAGS = $(WARN_CFLAGS)

gnome_session_SOURCES =				\
	gsm-app.h				\
	gsm-app.c				\
	gsm-autostart-app.h			\
	gsm-autostart-app.c			\
	gsm-client.c				\
	gsm-client.h				\
	gsm-xsmp-client.h			\
	gsm-xsmp-client.c			\
	gsm-dbus-client.h			\
	gsm-dbus-client.c			\
	gsm-marshal.h				\
	gsm-marshal.c				\
	gsm-consolekit.c			\
	gsm-consolekit.h			\
	gsm-logout-dialog.h			\
	gsm-logout-dialog.c			\
	gsm-inhibit-dialog.h			\
	gsm-inhibit-dialog.c			\
	gs-idle-monitor.h			\
	gs-idle-monitor.c			\
	gsm-presence.h				\
	gsm-presence.c				\
	gsm-gconf.c				\
	gsm-gconf.h				\
	gdm.h					\
	gdm.c					\
	gdm-signal-handler.h			\
	gdm-signal-handler.c			\
	gdm-log.h				\
	gdm-log.c				\
	main.c					\
	gsm-store.h				\
	gsm-store.c				\
	gsm-inhibitor.h				\
	gsm-inhibitor.c				\
	gsm-manager.c				\
	gsm-manager.h				\
	gsm-session-save.c			\
	gsm-session-save.h			\
	gsm-xsmp-server.c			\
	gsm-xsmp-server.h

gnome_session_CPPFLAGS =			\
	$(AM_CPPFLAGS)				\
	$(SM_CFLAGS)				\
	$(ICE_CFLAGS)				\
	$(XEXT_CFLAGS)				\
	$(GCONF_CFLAGS)				\
	-I$(top_srcdir)/egg			\
	-DLOCALE_DIR=\""$(datadir)/locale"\"	\
	-DDATA_DIR=\""$(datadir)/gnome-session"\" \
	-DLIBEXECDIR=\"$(libexecdir)\"		\
	-DGTKBUILDER_DIR=\""$(pkgdatadir)"\"	\
	-DGCONF_SANITY_CHECK=\""$(GCONF_SANITY_CHECK)"\" \
	-DGCONFTOOL_CMD=\"$(GCONFTOOL)\"	\
	-DI_KNOW_THE_DEVICEKIT_POWER_API_IS_SUBJECT_TO_CHANGE

gnome_session_LDADD =				\
	libgsmutil.la 				\
	$(top_builddir)/egg/libeggdesktopfile.la \
	$(SM_LIBS)				\
	$(ICE_LIBS)				\
	$(XRENDER_LIBS)				\
	$(XTEST_LIBS)				\
	$(XEXT_LIBS)				\
	$(GNOME_SESSION_LIBS)			\
	$(GCONF_LIBS)				\
	$(EXECINFO_LIBS)

libgsmutil_la_SOURCES =				\
	gsm-util.c				\
	gsm-util.h

libgsmutil_la_LIBADD = 				\
	$(GNOME_SESSION_LIBS)

test_inhibit_SOURCES = test-inhibit.c
test_inhibit_LDADD = $(GNOME_SESSION_LIBS)

test_client_dbus_SOURCES = test-client-dbus.c
test_client_dbus_LDADD = $(DBUS_GLIB_LIBS)

gsm-marshal.c: gsm-marshal.list
	$(AM_V_GEN)echo "#include \"gsm-marshal.h\"" > $@ && \
	$(GLIB_GENMARSHAL) $< --prefix=gsm_marshal --body >> $@

gsm-marshal.h: gsm-marshal.list
	$(AM_V_GEN)$(GLIB_GENMARSHAL) $< --prefix=gsm_marshal --header > $@

gsm-manager-glue.h: org.gnome.SessionManager.xml Makefile.am
	$(AM_V_GEN)dbus-binding-tool --prefix=gsm_manager --mode=glib-server --output=gsm-manager-glue.h $(srcdir)/org.gnome.SessionManager.xml

gsm-client-glue.h: org.gnome.SessionManager.Client.xml Makefile.am
	$(AM_V_GEN)dbus-binding-tool --prefix=gsm_client --mode=glib-server --output=gsm-client-glue.h $(srcdir)/org.gnome.SessionManager.Client.xml

gsm-app-glue.h: org.gnome.SessionManager.App.xml Makefile.am
	$(AM_V_GEN)dbus-binding-tool --prefix=gsm_app --mode=glib-server --output=gsm-app-glue.h $(srcdir)/org.gnome.SessionManager.App.xml

gsm-inhibitor-glue.h: org.gnome.SessionManager.Inhibitor.xml Makefile.am
	$(AM_V_GEN)dbus-binding-tool --prefix=gsm_inhibitor --mode=glib-server --output=gsm-inhibitor-glue.h $(srcdir)/org.gnome.SessionManager.Inhibitor.xml

gsm-presence-glue.h: org.gnome.SessionManager.Presence.xml Makefile.am
	$(AM_V_GEN)dbus-binding-tool --prefix=gsm_presence --mode=glib-server --output=gsm-presence-glue.h $(srcdir)/org.gnome.SessionManager.Presence.xml

BUILT_SOURCES =			\
	gsm-marshal.c		\
	gsm-marshal.h		\
	gsm-manager-glue.h	\
	gsm-presence-glue.h	\
	gsm-inhibitor-glue.h	\
	gsm-client-glue.h	\
	gsm-app-glue.h

EXTRA_DIST =						\
	README						\
	gsm-marshal.list				\
	org.gnome.SessionManager.xml			\
	org.gnome.SessionManager.App.xml		\
	org.gnome.SessionManager.Client.xml		\
	org.gnome.SessionManager.ClientPrivate.xml	\
	org.gnome.SessionManager.Inhibitor.xml		\
	org.gnome.SessionManager.Presence.xml

CLEANFILES =	\
	$(BUILT_SOURCES)

-include $(top_srcdir)/git.mk
