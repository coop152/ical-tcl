bin_PROGRAMS = ical
icallibdir = $(pkglibdir)/v@PACKAGE_VERSION@
nobase_dist_icallib_DATA = @ICAL_SCRIPTS@ $(srcdir)/tclIndex \
	       @ICAL_TCLLIB_SCRIPTS@ $(srcdir)/tcllib/tclIndex \
	       @ICAL_CONTRIB@
icallib_DATA = $(builddir)/startup.tcl $(builddir)/ps_header.tcl
EXTRA_DIST = startup.tcl.in ps_header.ps doc/ical.html doc/interface.html \
	     COPYRIGHT.ORIG Makefile.am
dist_man1_MANS = doc/ical.man

appdir = $(prefix)/share/applications
app_DATA = ical.desktop
ical_SOURCES = cal_tcl.cpp dateeditor.cpp dispatch.cpp ical.cpp ical_tcl.cpp \
	       item_tcl.cpp object.cpp time_tcl.cpp main.cpp
ical_CPPFLAGS = -DICALLIBDIR='"$(icallibdir)"' -I$(srcdir)/calendar -I$(srcdir)/types -I$(srcdir)/time @TK_XINCLUDES@
ical_LDADD = libcalendar.a libtime.a libtypes.a \
	     @TK_LIB_SPEC@ @TCL_LIB_SPEC@ @TK_LIBS@
ical_LDFLAGS = -mwindows

noinst_LIBRARIES = libcalendar.a libtime.a libtypes.a

libcalendar_a_CPPFLAGS = -I$(srcdir)/types -I$(srcdir)/time
libcalendar_a_SOURCES = calendar/arrays.cpp calendar/calendar.cpp \
			calendar/calfile.cpp calendar/dateset.cpp \
			calendar/item.cpp calendar/lexer.cpp calendar/misc.cpp \
			calendar/options.cpp calendar/smallintset.cpp \
			calendar/uid.cpp

libtime_a_SOURCES = time/Date.cpp time/Month.cpp time/Time.cpp time/WeekDay.cpp \
		    time/Year.cpp time/parse.cpp

libtypes_a_SOURCES = types/bitvec.cpp types/hashfuncs.cpp types/intset.cpp

CLEANFILES = $(icallib_DATA) $(app_DATA)

ps_header.tcl: ps_header.ps
	echo  'proc ps_header {} { set val {}' > $@;
	@SED@ -e 's/\[/\\[/g' \
	      -e 's/"/\\"/g' \
	      -e 's/.*/  set val "$$val&\\n"/' < $< >> $@;
	echo '  return $$val\n}' >> $@

ical.desktop:
	echo "[Desktop Entry]" >$@
	echo "Name=Ical" >>$@
	echo "Comment=Ical calendar package" >>$@
	echo "Exec=ical" >>$@
	echo  'Icon=$(icallibdir)/contrib/ical_icon.png' >>$@
	echo "Terminal=false" >>$@
	echo "Type=Application" >>$@
	echo "Categories=Office" >>$@
	echo "StartupNotify=true;" >>$@
	chmod 644 $@

# cannot do it in configure, as libdir is not known there :(
startup.tcl: startup.tcl.in
	@SED@ -e 's!@''PACKAGE_VERSION''@!@PACKAGE_VERSION@!g' \
	      -e 's!@''MAILER''@!@MAILER@!g' \
	      -e 's!@''pkglibdir''@!$(pkglibdir)!g' \
	      -e 's!@''icallibdir''@!$(icallibdir)!g' < $< > $@

noinst_HEADERS = cal_tcl.h calendar/arrays.h calendar/calendar.h \
		 calendar/calfile.h calendar/dateset.h \
		 calendar/item.h calendar/itemmap.h calendar/lexer.h \
		 calendar/misc.h calendar/options.h calendar/smallintset.h \
		 calendar/statfix.h calendar/uid.h calendar/version.h \
		 collect.h config.h dispatch.h ical.h item_tcl.h object.h \
		 types/Array.h types/basic.h time/Date.h time/Month.h \
		 time/Time_.h time/WeekDay.h time/Year.h time/parse.h \
		 types/Array.h types/basic.h types/bitvec.h types/hashfuncs.h \
		 types/htable.h types/htable_p.h types/intset.h \
		 types/ohashmap.h types/ohashset.h types/tablerep.h \
		 bitmaps/left.xbm bitmaps/right.xbm bitmaps/todo.xbm \
		 bitmaps/done.xbm bitmaps/sleft.xbm bitmaps/dleft.xbm \
		 bitmaps/sright.xbm bitmaps/ical.xbm bitmaps/dright.xbm
