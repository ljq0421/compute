#  Copyright (c) 1993, 1994, 1995, 1996
# 	The Regents of the University of California.  All rights reserved.
#
#  Redistribution and use in source and binary forms, with or without
#  modification, are permitted provided that: (1) source code distributions
#  retain the above copyright notice and this paragraph in its entirety, (2)
#  distributions including binary code include the above copyright notice and
#  this paragraph in its entirety in the documentation or other materials
#  provided with the distribution, and (3) all advertising materials mentioning
#  features or use of this software display the following acknowledgement:
#  ``This product includes software developed by the University of California,
#  Lawrence Berkeley Laboratory and its contributors.'' Neither the name of
#  the University nor the names of its contributors may be used to endorse
#  or promote products derived from this software without specific prior
#  written permission.
#  THIS SOFTWARE IS PROVIDED ``AS IS'' AND WITHOUT ANY EXPRESS OR IMPLIED
#  WARRANTIES, INCLUDING, WITHOUT LIMITATION, THE IMPLIED WARRANTIES OF
#  MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE.

#
# Various configurable paths (remember to edit Makefile.in, not Makefile)
#

# Top level hierarchy
prefix = /usr/local
exec_prefix = ${prefix}
datarootdir = ${prefix}/share
# Pathname of directory to install the configure program
bindir = ${exec_prefix}/bin
# Pathname of directory to install the include files
includedir = ${prefix}/include
# Pathname of directory to install the library
libdir =  ${exec_prefix}/lib
# Pathname of directory to install the man pages
mandir = ${datarootdir}/man

# VPATH
srcdir = .


#
# You shouldn't need to edit anything below.
#

LD = /usr/bin/ld
CC = gcc
AR = ar
LN_S = ln -s
MKDEP = 
CCOPT =  -fvisibility=hidden -fpic
PF_RING_INCLUDES=-I ../../kernel -I ../lib
PF_RING_LIBS= ../lib/libpfring.a -lpthread -lrt
INCLS = -I. $(PF_RING_INCLUDES) 
DEFS = -DBUILDING_PCAP -DHAVE_CONFIG_H  -D_U_="__attribute__((unused))" -DHAVE_PF_RING 
MACHINE=$(shell uname -m) # HAVE_PF_RING
ADDLOBJS = 
ADDLARCHIVEOBJS = 
LIBS = $(PF_RING_LIBS)   -lrt -ldl
CROSSFLAGS=
CFLAGS = -g -O2   ${CROSSFLAGS}
LDFLAGS =  ${CROSSFLAGS}
DYEXT = so
V_RPATH_OPT = -Wl,-rpath,
DEPENDENCY_CFLAG = 
PROG=libpcap

# Standard CFLAGS
FULL_CFLAGS = $(CCOPT) $(INCLS) $(DEFS) $(CFLAGS)

INSTALL = /usr/bin/install -c
INSTALL_PROGRAM = ${INSTALL}
INSTALL_DATA = ${INSTALL} -m 644
RANLIB = ranlib

LEX = flex
YACC = bison -y

# Explicitly define compilation rule since SunOS 4's make doesn't like gcc.
# Also, gcc does not remove the .o before forking 'as', which can be a
# problem if you don't own the file but can write to the directory.
.c.o:
	@rm -f $@
	$(CC) $(FULL_CFLAGS) -c $(srcdir)/$*.c

PSRC =	pcap-linux.c pcap-usb-linux.c   pcap-netfilter-linux.c 
FSRC =  fad-getad.c
SSRC =  
CSRC =	pcap.c inet.c fad-helpers.c gencode.c optimize.c nametoaddr.c \
	etherent.c savefile.c sf-pcap.c sf-pcap-ng.c pcap-common.c \
	bpf_image.c bpf_dump.c
GENSRC = scanner.c grammar.c bpf_filter.c version.c
LIBOBJS = 

SRC =	$(PSRC) $(FSRC) $(CSRC) $(SSRC) $(GENSRC)

# We would like to say "OBJ = $(SRC:.c=.o)" but Ultrix's make cannot
# hack the extra indirection
OBJ =	$(PSRC:.c=.o) $(FSRC:.c=.o) $(CSRC:.c=.o) $(SSRC:.c=.o) $(GENSRC:.c=.o) $(LIBOBJS)
PUBHDR = \
	pcap.h \
	pcap-bpf.h \
	pcap-namedb.h \
	pcap/bpf.h \
	pcap/bluetooth.h \
	pcap/can_socketcan.h \
	pcap/dlt.h \
	pcap/export-defs.h \
	pcap/ipnet.h \
	pcap/namedb.h \
	pcap/nflog.h \
	pcap/pcap.h \
	pcap/sll.h \
	pcap/vlan.h \
	pcap/usb.h

HDR = $(PUBHDR) \
	arcnet.h \
	atmuni31.h \
	ethertype.h \
	extract.h \
	gencode.h \
	ieee80211.h \
	llc.h \
	nametoaddr.h \
	nlpid.h \
	pcap-common.h \
	pcap-int.h \
	pcap-stdinc.h \
	portability.h \
	ppp.h \
	sf-pcap.h \
	sf-pcap-ng.h \
	sunatmpos.h

TESTS = \
	valgrindtest \
	capturetest \
	can_set_rfmon_test \
	filtertest \
	findalldevstest \
	opentest \
	reactivatetest \
	selpolltest

TESTS_SRC = \
	tests/valgrindtest.c \
	tests/capturetest.c \
	tests/can_set_rfmon_test.c \
	tests/filtertest.c \
	tests/findalldevstest.c \
	tests/opentest.c \
	tests/reactivatetest.c \
	tests/selpolltest.c

GENHDR = \
	scanner.h grammar.h pcap_version.h

TAGFILES = \
	$(SRC) $(HDR)

CLEANFILES = $(OBJ) libpcap.* $(TESTS) \
	$(PROG)-`cat $(srcdir)/VERSION`.tar.gz $(GENSRC) $(GENHDR) \
	lex.yy.c pcap-config

MAN1 = pcap-config.1

MAN3PCAP_EXPAND = \
	pcap.3pcap.in \
	pcap_compile.3pcap.in \
	pcap_datalink.3pcap.in \
	pcap_dump_open.3pcap.in \
	pcap_get_tstamp_precision.3pcap.in \
	pcap_list_datalinks.3pcap.in \
	pcap_list_tstamp_types.3pcap.in \
	pcap_open_dead.3pcap.in \
	pcap_open_offline.3pcap.in \
	pcap_set_tstamp_precision.3pcap.in \
	pcap_set_tstamp_type.3pcap.in

MAN3PCAP_NOEXPAND = \
	pcap_activate.3pcap \
	pcap_breakloop.3pcap \
	pcap_can_set_rfmon.3pcap \
	pcap_close.3pcap \
	pcap_create.3pcap \
	pcap_datalink_name_to_val.3pcap \
	pcap_datalink_val_to_name.3pcap \
	pcap_dump.3pcap \
	pcap_dump_close.3pcap \
	pcap_dump_file.3pcap \
	pcap_dump_flush.3pcap \
	pcap_dump_ftell.3pcap \
	pcap_file.3pcap \
	pcap_fileno.3pcap \
	pcap_findalldevs.3pcap \
	pcap_freecode.3pcap \
	pcap_get_selectable_fd.3pcap \
	pcap_geterr.3pcap \
	pcap_inject.3pcap \
	pcap_is_swapped.3pcap \
	pcap_lib_version.3pcap \
	pcap_lookupdev.3pcap \
	pcap_lookupnet.3pcap \
	pcap_loop.3pcap \
	pcap_major_version.3pcap \
	pcap_next_ex.3pcap \
	pcap_offline_filter.3pcap \
	pcap_open_live.3pcap \
	pcap_set_buffer_size.3pcap \
	pcap_set_datalink.3pcap \
	pcap_set_immediate_mode.3pcap \
	pcap_set_promisc.3pcap \
	pcap_set_rfmon.3pcap \
	pcap_set_snaplen.3pcap \
	pcap_set_timeout.3pcap \
	pcap_setdirection.3pcap \
	pcap_setfilter.3pcap \
	pcap_setnonblock.3pcap \
	pcap_snapshot.3pcap \
	pcap_stats.3pcap \
	pcap_statustostr.3pcap \
	pcap_strerror.3pcap \
	pcap_tstamp_type_name_to_val.3pcap \
	pcap_tstamp_type_val_to_name.3pcap

MAN3PCAP = $(MAN3PCAP_NOEXPAND) $(MAN3PCAP_EXPAND:.in=)

MANFILE = \
	pcap-savefile.manfile.in

MANMISC = \
	pcap-filter.manmisc.in \
	pcap-linktype.manmisc.in \
	pcap-tstamp.manmisc.in

EXTRA_DIST = \
	$(TESTS_SRC) \
	CHANGES \
	ChmodBPF/ChmodBPF \
	ChmodBPF/StartupParameters.plist \
	CREDITS \
	CMakeLists.txt \
	GenVersion.bat \
	INSTALL.txt \
	LICENSE \
	Makefile.in \
	Makefile-devel-adds \
	README \
	README.aix \
	README.dag \
	README.hpux \
	README.linux \
	README.macosx \
	README.septel \
	README.sita \
	README.tru64 \
	README.Win32 \
	SUNOS4/nit_if.o.sparc \
	SUNOS4/nit_if.o.sun3 \
	SUNOS4/nit_if.o.sun4c.4.0.3c \
	TODO \
	VERSION \
	aclocal.m4 \
	bpf/net/bpf_filter.c \
	chmod_bpf \
	cmakeconfig.h.in \
	cmake/preconfigure.cmake \
	config/have_siocglifconf.c \
	config.guess \
	config.h.in \
	config.sub \
	configure \
	configure.ac \
	dlpisubs.c \
	dlpisubs.h \
	fad-getad.c \
	fad-gifc.c \
	fad-glifc.c \
	fad-helpers.c \
	gen_version_c.sh \
	gen_version_header.sh \
	grammar.y \
	install-sh \
	lbl/os-aix4.h \
	lbl/os-aix7.h \
	lbl/os-hpux11.h \
	lbl/os-osf4.h \
	lbl/os-osf5.h \
	lbl/os-solaris2.h \
	lbl/os-sunos4.h \
	lbl/os-ultrix4.h \
	missing/getopt.c \
	missing/getopt.h \
	missing/snprintf.c \
	missing/strtok_r.c \
	missing/win_snprintf.c \
	mkdep \
	msdos/bin2c.c \
	msdos/common.dj \
	msdos/makefile \
	msdos/makefile.dj \
	msdos/makefile.wc \
	msdos/ndis2.c \
	msdos/ndis2.h \
	msdos/ndis_0.asm \
	msdos/pkt_rx0.asm \
	msdos/pkt_rx1.s \
	msdos/pktdrvr.c \
	msdos/pktdrvr.h \
	msdos/readme.dos \
	org.tcpdump.chmod_bpf.plist \
	pcap-bpf.c \
	pcap-bt-linux.c \
	pcap-bt-linux.h \
	pcap-bt-monitor-linux.c \
	pcap-bt-monitor-linux.h \
	pcap-config.in \
	pcap-dag.c \
	pcap-dag.h \
	pcap-dbus.c \
	pcap-dbus.h \
	pcap-dlpi.c \
	pcap-dos.c \
	pcap-dos.h \
	pcap-enet.c \
	pcap-int.h \
	pcap-libdlpi.c \
	pcap-linux.c \
	pcap-namedb.h \
	pcap-new.c \
	pcap-netfilter-linux.c \
	pcap-netfilter-linux.h \
	pcap-nit.c \
	pcap-null.c \
	pcap-pf.c \
	pcap-rpcap.c \
	pcap-rpcap.h \
	pcap-septel.c \
	pcap-septel.h \
	pcap-sita.h \
	pcap-sita.c \
	pcap-sita.html \
	pcap-snf.c \
	pcap-snf.h \
	pcap-snit.c \
	pcap-snoop.c \
	pcap-tc.c \
	pcap-tc.h \
	pcap-usb-linux.c \
	pcap-usb-linux.h \
	pcap-win32.c \
	remote-ext.h \
	sockutils.c \
	sockutils.h \
	scanner.l \
	tests/CMakeLists.txt \
	pcap_version.h.in \
	Win32/Include/Gnuc.h \
	Win32/Include/net/if.h \
	Win32/Prj/wpcap.sln \
	Win32/Prj/wpcap.vcxproj \
	Win32/Prj/wpcap.vcxproj.filters

all: libpcap.a shared pcap-config

libpcap.a: $(OBJ)
	@rm -f $@
	$(AR) rc $@ $(OBJ) $(ADDLARCHIVEOBJS)
	$(RANLIB) $@

shared: libpcap.$(DYEXT)

libpcap.so: $(OBJ)
	@rm -f $@
	VER=`cat $(srcdir)/VERSION`; \
	MAJOR_VER=`sed 's/\([0-9][0-9]*\)\..*/\1/' $(srcdir)/VERSION`; \
	$(CC) -shared -Wl,-soname,$@.$$MAJOR_VER $(LDFLAGS) \
	    -o $@.$$VER $(OBJ) $(ADDLOBJS) $(LIBS)

#
# The following rule succeeds, but the result is untested.
#
# In Mac OS X, the libpcap dylib has the name "libpcap.A.dylib", with
# its full path as the install_name, and with the compatibility and
# current version both set to 1.  The compatibility version is set to
# 1 so that programs built with a newer version of the library will run
# against older versions; multi-platform software probably will fail if
# it uses APIs added in the newer version, but Mac OS X-specific software
# will use weak linking and check at run time whether those APIs are
# available.
#
# We also use "A" as the major version, and 1 as the compatibility version,
# but set the current version to the value in VERSION, with any non-numeric
# stuff stripped off (the compatibility and current version must be of the
# form X[.Y[.Z]], with Y and Z possibly absent, and with all components
# numeric).
#
libpcap.dylib: $(OBJ)
	rm -f libpcap*.dylib
	VER=`cat $(srcdir)/VERSION`; \
	MAJOR_VER=A; \
	COMPAT_VER=1; \
	CURRENT_VER=`sed 's/[^0-9.].*$$//' $(srcdir)/VERSION`; \
	$(CC) -dynamiclib -undefined error $(LDFLAGS) \
	    -o libpcap.$$VER.dylib $(OBJ) $(ADDLOBJS) $(LIBS) \
	    -install_name $(libdir)/libpcap.$$MAJOR_VER.dylib \
	    -compatibility_version $$COMPAT_VER \
	    -current_version $$CURRENT_VER

#
# The HP-UX linker manual says that the convention for a versioned library
# is libXXX.{number}, not libXXX.sl.{number}.  That appears to be the case
# on at least one HP-UX 11.00 system; libXXX.sl is a symlink to
# libXXX.{number}.
#
# The manual also says "library-level versioning" (think "sonames") was
# added in HP-UX 10.0.
#
# XXX - this assumes we're using the HP linker, rather than the GNU
# linker, even with GCC.
#
libpcap.sl: $(OBJ)
	@MAJOR_VER=`sed 's/\([0-9][0-9]*\)\..*/\1/' $(srcdir)/VERSION`; \
	rm -f libpcap.$$MAJOR_VER
	MAJOR_VER=`sed 's/\([0-9][0-9]*\)\..*/\1/' $(srcdir)/VERSION`; \
	ld -b $(LDFLAGS) -o libpcap.$$MAJOR_VER +h libpcap.$$MAJOR_VER \
	    $(OBJ) $(ADDLOBJS) $(LIBS)

#
# AIX is different from everybody else.  A shared library is an archive
# library with one or more shared-object components.  We still build a
# normal static archive library on AIX, for the benefit of the traditional
# scheme of building libpcap and tcpdump in subdirectories of the
# same directory, with tcpdump statically linked with the libpcap
# in question, but we also build a shared library as "libpcap.shareda"
# and install *it*, rather than the static library, as "libpcap.a".
#
libpcap.shareda: $(OBJ)
	@rm -f $@ shr.o
	$(CC) -shared -o shr.o $(OBJ) $(ADDLOBJS) $(LDFLAGS) $(LIBS)
	$(AR) rc $@ shr.o

#
# For platforms that don't support shared libraries (or on which we
# don't support shared libraries).
#
libpcap.none:

scanner.c: $(srcdir)/scanner.l
	$(LEX) -P pcap_ --header-file=scanner.h --nounput -o scanner.c $<
scanner.h: scanner.c
## Recover from the removal of $@
	@if test -f $@; then :; else \
		rm -f scanner.c; \
		$(MAKE) $(MAKEFLAGS) scanner.c; \
	fi

scanner.o: scanner.c grammar.h
	$(CC) $(FULL_CFLAGS) -c scanner.c

pcap.o: pcap_version.h

grammar.c: $(srcdir)/grammar.y
	$(YACC) -p pcap_ -o grammar.c -d $<
grammar.h: grammar.c
## Recover from the removal of $@
	@if test -f $@; then :; else \
		rm -f grammar.c; \
		$(MAKE) $(MAKEFLAGS) grammar.c; \
	fi

grammar.o: grammar.c
	$(CC) $(FULL_CFLAGS) -c grammar.c

gencode.o: $(srcdir)/gencode.c grammar.h scanner.h
	$(CC) $(FULL_CFLAGS) -c $(srcdir)/gencode.c

version.o: version.c
	$(CC) $(FULL_CFLAGS) -c version.c

snprintf.o: $(srcdir)/missing/snprintf.c
	$(CC) $(FULL_CFLAGS) -o $@ -c $(srcdir)/missing/snprintf.c

strtok_r.o: $(srcdir)/missing/strtok_r.c
	$(CC) $(FULL_CFLAGS) -o $@ -c $(srcdir)/missing/strtok_r.c

version.c: $(srcdir)/VERSION $(srcdir)/gen_version_c.sh
	#
	# Older programs import this if they want to show the
	# libpcap version number, rather than calling
	# pcap_lib_version(), so we need to export it.
	#
	@rm -f $@
	$(srcdir)/gen_version_c.sh $(srcdir)/VERSION $@

pcap_version.h: $(srcdir)/VERSION $(srcdir)/pcap_version.h.in $(srcdir)/gen_version_header.sh
	@rm -f $@
	$(srcdir)/gen_version_header.sh $(srcdir)/VERSION $(srcdir)/pcap_version.h.in $@

bpf_filter.c: $(srcdir)/bpf/net/bpf_filter.c
	rm -f bpf_filter.c
	ln -s $(srcdir)/bpf/net/bpf_filter.c bpf_filter.c

bpf_filter.o: bpf_filter.c
	$(CC) $(FULL_CFLAGS) -c bpf_filter.c

#
# Generate the pcap-config script.
#
# Some Makes, e.g. AIX Make and Solaris Make, can't handle "--file=$@.tmp:$<";
# for example, the Solaris 9 make man page says
#
#	Because make assigns $< and $* as it would for implicit rules
#	(according to the suffixes list and the directory contents),
#	they may be unreliable when used within explicit target entries.
#
# and this is an explicit target entry.
#
# Therefore, instead of using $<, we explicitly put in $(srcdir)/pcap-config.in.
#
pcap-config: $(srcdir)/pcap-config.in ./config.status
	@rm -f $@ $@.tmp
	./config.status --file=$@.tmp:$(srcdir)/pcap-config.in
	mv $@.tmp $@
	chmod a+x $@

#
# Test programs - not built by default, and not installed.
#
tests: $(TESTS)

capturetest: tests/capturetest.c libpcap.a
	$(CC) $(FULL_CFLAGS) -I. -L. -o capturetest $(srcdir)/tests/capturetest.c libpcap.a $(LIBS)

can_set_rfmon_test: tests/can_set_rfmon_test.c libpcap.a
	$(CC) $(FULL_CFLAGS) -I. -L. -o can_set_rfmon_test $(srcdir)/tests/can_set_rfmon_test.c libpcap.a $(LIBS)

filtertest: tests/filtertest.c libpcap.a
	$(CC) $(FULL_CFLAGS) -I. -L. -o filtertest $(srcdir)/tests/filtertest.c libpcap.a $(LIBS)

findalldevstest: tests/findalldevstest.c libpcap.a
	$(CC) $(FULL_CFLAGS) -I. -L. -o findalldevstest $(srcdir)/tests/findalldevstest.c libpcap.a $(LIBS)

opentest: tests/opentest.c libpcap.a
	$(CC) $(FULL_CFLAGS) -I. -L. -o opentest $(srcdir)/tests/opentest.c libpcap.a $(LIBS)

reactivatetest: tests/reactivatetest.c libpcap.a
	$(CC) $(FULL_CFLAGS) -I. -L. -o reactivatetest $(srcdir)/tests/reactivatetest.c libpcap.a $(LIBS)

selpolltest: tests/selpolltest.c libpcap.a
	$(CC) $(FULL_CFLAGS) -I. -L. -o selpolltest $(srcdir)/tests/selpolltest.c libpcap.a $(LIBS)

valgrindtest: tests/valgrindtest.c libpcap.a
	$(CC) $(FULL_CFLAGS) -I. -L. -o valgrindtest $(srcdir)/tests/valgrindtest.c libpcap.a $(LIBS)

install: install-shared install-archive pcap-config
	[ -d $(DESTDIR)$(libdir) ] || \
	    (mkdir -p $(DESTDIR)$(libdir); chmod 755 $(DESTDIR)$(libdir))
	[ -d $(DESTDIR)$(includedir) ] || \
	    (mkdir -p $(DESTDIR)$(includedir); chmod 755 $(DESTDIR)$(includedir))
	[ -d $(DESTDIR)$(includedir)/pcap ] || \
	    (mkdir -p $(DESTDIR)$(includedir)/pcap; chmod 755 $(DESTDIR)$(includedir)/pcap)
	[ -d $(DESTDIR)$(mandir)/man1 ] || \
	    (mkdir -p $(DESTDIR)$(mandir)/man1; chmod 755 $(DESTDIR)$(mandir)/man1)
	[ -d $(DESTDIR)$(mandir)/man3 ] || \
	    (mkdir -p $(DESTDIR)$(mandir)/man3; chmod 755 $(DESTDIR)$(mandir)/man3)
	[ -d $(DESTDIR)$(mandir)/man5 ] || \
	    (mkdir -p $(DESTDIR)$(mandir)/man5; chmod 755 $(DESTDIR)$(mandir)/man5)
	[ -d $(DESTDIR)$(mandir)/man7 ] || \
	    (mkdir -p $(DESTDIR)$(mandir)/man7; chmod 755 $(DESTDIR)$(mandir)/man7)
	for i in $(PUBHDR); do \
		$(INSTALL_DATA) $(srcdir)/$$i \
		    $(DESTDIR)$(includedir)/$$i; done
	[ -d $(DESTDIR)$(bindir) ] || \
	    (mkdir -p $(DESTDIR)$(bindir); chmod 755 $(DESTDIR)$(bindir))
	$(INSTALL_PROGRAM) pcap-config $(DESTDIR)$(bindir)/pcap-config
	for i in $(MAN1); do \
		$(INSTALL_DATA) $(srcdir)/$$i \
		    $(DESTDIR)$(mandir)/man1/$$i; done
	for i in $(MANFILE); do \
		$(INSTALL_DATA) `echo $$i | sed 's/.manfile.in/.manfile/'` \
		    $(DESTDIR)$(mandir)/man5/`echo $$i | sed 's/.manfile.in/.5/'`; done
	for i in $(MANMISC); do \
		$(INSTALL_DATA) `echo $$i | sed 's/.manmisc.in/.manmisc/'` \
		    $(DESTDIR)$(mandir)/man7/`echo $$i | sed 's/.manmisc.in/.7/'`; done

install-shared: install-shared-$(DYEXT)
install-shared-so: libpcap.so
	[ -d $(DESTDIR)$(libdir) ] || \
	    (mkdir -p $(DESTDIR)$(libdir); chmod 755 $(DESTDIR)$(libdir))
	VER=`cat $(srcdir)/VERSION`; \
	MAJOR_VER=`sed 's/\([0-9][0-9]*\)\..*/\1/' $(srcdir)/VERSION`; \
	$(INSTALL_PROGRAM) libpcap.so.$$VER $(DESTDIR)$(libdir)/libpcap.so.$$VER; \
	ln -sf libpcap.so.$$VER $(DESTDIR)$(libdir)/libpcap.so.$$MAJOR_VER; \
	ln -sf libpcap.so.$$MAJOR_VER $(DESTDIR)$(libdir)/libpcap.so
install-shared-dylib: libpcap.dylib
	[ -d $(DESTDIR)$(libdir) ] || \
	    (mkdir -p $(DESTDIR)$(libdir); chmod 755 $(DESTDIR)$(libdir))
	VER=`cat $(srcdir)/VERSION`; \
	MAJOR_VER=A; \
	$(INSTALL_PROGRAM) libpcap.$$VER.dylib $(DESTDIR)$(libdir)/libpcap.$$VER.dylib; \
	ln -sf libpcap.$$VER.dylib $(DESTDIR)$(libdir)/libpcap.$$MAJOR_VER.dylib; \
	ln -sf libpcap.$$MAJOR_VER.dylib $(DESTDIR)$(libdir)/libpcap.dylib
install-shared-sl: libpcap.sl
	[ -d $(DESTDIR)$(libdir) ] || \
	    (mkdir -p $(DESTDIR)$(libdir); chmod 755 $(DESTDIR)$(libdir))
	MAJOR_VER=`sed 's/\([0-9][0-9]*\)\..*/\1/' $(srcdir)/VERSION`; \
	$(INSTALL_PROGRAM) libpcap.$$MAJOR_VER $(DESTDIR)$(libdir)
	ln -sf libpcap.$$MAJOR_VER $(DESTDIR)$(libdir)/libpcap.sl
install-shared-shareda: libpcap.shareda
	#
	# AIX shared libraries are weird.  They're archive libraries
	# with one or more shared object components.
	#
	[ -d $(DESTDIR)$(libdir) ] || \
	    (mkdir -p $(DESTDIR)$(libdir); chmod 755 $(DESTDIR)$(libdir))
	$(INSTALL_PROGRAM) libpcap.shareda $(DESTDIR)$(libdir)/libpcap.a
install-shared-none:

install-archive: install-archive-$(DYEXT)
install-archive-so install-archive-dylib install-archive-sl install-archive-none: libpcap.a
	#
	# Most platforms have separate suffixes for shared and
	# archive libraries, so we install both.
	#
	[ -d $(DESTDIR)$(libdir) ] || \
	    (mkdir -p $(DESTDIR)$(libdir); chmod 755 $(DESTDIR)$(libdir))
	$(INSTALL_DATA) libpcap.a $(DESTDIR)$(libdir)/libpcap.a
	$(RANLIB) $(DESTDIR)$(libdir)/libpcap.a
install-archive-shareda:
	#
	# AIX, however, doesn't, so we don't install the archive
	# library on AIX.
	#

uninstall: uninstall-shared
	rm -f $(DESTDIR)$(libdir)/libpcap.a
	for i in $(PUBHDR); do \
		rm -f $(DESTDIR)$(includedir)/$$i; done
	-rmdir $(DESTDIR)$(includedir)/pcap
	rm -f $(DESTDIR)/$(bindir)/pcap-config
	for i in $(MAN1); do \
		rm -f $(DESTDIR)$(mandir)/man1/$$i; done
	for i in $(MAN3PCAP); do \
		rm -f $(DESTDIR)$(mandir)/man3/$$i; done
	rm -f $(DESTDIR)$(mandir)/man3/pcap_datalink_val_to_description.3pcap
	rm -f $(DESTDIR)$(mandir)/man3/pcap_dump_fopen.3pcap
	rm -f $(DESTDIR)$(mandir)/man3/pcap_freealldevs.3pcap
	rm -f $(DESTDIR)$(mandir)/man3/pcap_perror.3pcap
	rm -f $(DESTDIR)$(mandir)/man3/pcap_sendpacket.3pcap
	rm -f $(DESTDIR)$(mandir)/man3/pcap_free_datalinks.3pcap
	rm -f $(DESTDIR)$(mandir)/man3/pcap_free_tstamp_types.3pcap
	rm -f $(DESTDIR)$(mandir)/man3/pcap_dispatch.3pcap
	rm -f $(DESTDIR)$(mandir)/man3/pcap_minor_version.3pcap
	rm -f $(DESTDIR)$(mandir)/man3/pcap_next.3pcap
	rm -f $(DESTDIR)$(mandir)/man3/pcap_open_dead_with_tstamp_precision.3pcap
	rm -f $(DESTDIR)$(mandir)/man3/pcap_open_offline_with_tstamp_precision.3pcap
	rm -f $(DESTDIR)$(mandir)/man3/pcap_fopen_offline.3pcap
	rm -f $(DESTDIR)$(mandir)/man3/pcap_fopen_offline_with_tstamp_precision.3pcap
	rm -f $(DESTDIR)$(mandir)/man3/pcap_getnonblock.3pcap
	rm -f $(DESTDIR)$(mandir)/man3/pcap_tstamp_type_val_to_description.3pcap
	for i in $(MANFILE); do \
		rm -f $(DESTDIR)$(mandir)/man5/`echo $$i | sed 's/.manfile.in/.5/'`; done
	for i in $(MANMISC); do \
		rm -f $(DESTDIR)$(mandir)/man7/`echo $$i | sed 's/.manmisc.in/.7/'`; done

uninstall-shared: uninstall-shared-$(DYEXT)
uninstall-shared-so:
	VER=`cat $(srcdir)/VERSION`; \
	MAJOR_VER=`sed 's/\([0-9][0-9]*\)\..*/\1/' $(srcdir)/VERSION`; \
	rm -f $(DESTDIR)$(libdir)/libpcap.so.$$VER; \
	rm -f $(DESTDIR)$(libdir)/libpcap.so.$$MAJOR_VER; \
	rm -f $(DESTDIR)$(libdir)/libpcap.so
uninstall-shared-dylib:
	VER=`cat $(srcdir)/VERSION`; \
	MAJOR_VER=A; \
	rm -f $(DESTDIR)$(libdir)/libpcap.$$VER.dylib; \
	rm -f $(DESTDIR)$(libdir)/libpcap.$$MAJOR_VER.dylib; \
	rm -f $(DESTDIR)$(libdir)/libpcap.dylib
uninstall-shared-sl:
	MAJOR_VER=`sed 's/\([0-9][0-9]*\)\..*/\1/' $(srcdir)/VERSION`; \
	rm -f $(DESTDIR)$(libdir)/libpcap.$$MAJOR_VER; \
	rm -f $(DESTDIR)$(libdir)/libpcap.sl
uninstall-shared-shareda:
	rm -f $(DESTDIR)$(libdir)/libpcap.a
uninstall-shared-none:

clean:
	rm -f $(CLEANFILES)

distclean: clean
	rm -f Makefile config.cache config.log config.status \
	    config.h gnuc.h net os-proto.h bpf_filter.c pcap-config \
	    stamp-h stamp-h.in
	rm -f $(MAN3PCAP_EXPAND:.in=) $(MANFILE:.in=) $(MANMISC:.in=)
	rm -rf autom4te.cache

extags: $(TAGFILES)
	ctags $(TAGFILES)

tags: $(TAGFILES)
	ctags -wtd $(TAGFILES)

releasetar:
	@cwd=`pwd` ; dir=`basename $$cwd` ; name=$(PROG)-`cat VERSION` ; \
	   mkdir $$name; \
	   tar cf - $(CSRC) $(HDR) $(MAN1) $(MAN3PCAP_EXPAND) \
	      $(MAN3PCAP_NOEXPAND) $(MANFILE) $(MANMISC) $(EXTRA_DIST) | \
	      (cd $$name; tar xf -); \
	   tar -c -z -f $$name.tar.gz $$name; \
	   rm -rf $$name

depend:	$(GENSRC) $(GENHDR) bpf_filter.c
	$(MKDEP) -c $(CC) -m $(CFLAGS) $(DEPENDENCY_CFLAG) $(DEFS) $(INCLS) $(SRC)
