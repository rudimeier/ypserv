#
# Copyright (c) 2000, 2001, 2003, 2007, 2016 Thorsten Kukuk <kukuk@linux-nis.org>
#
AUTOMAKE_OPTIONS = 1.7 gnits

localedir = $(datadir)/locale

DEFS = @DEFS@ -DLOCALEDIR=\"$(localedir)\" -DYPBINDIR=\"$(libexecdir)\" \
	-DCONFDIR=\"$(sysconfdir)\" -DYPMAPDIR=\"@YPMAPDIR@\" \
	-DUSE_FQDN=@USE_FQDN@
AM_CPPFLAGS = -I$(top_srcdir)/lib -I$(top_srcdir) -I$(top_builddir) \
	-I$(srcdir) @TIRPC_CFLAGS@ @NSL_CFLAGS@

CLEANFILES = *~

EXTRA_DIST = ${MANS} ${XMLS}

man_MANS = makedbm.8
XMLS = makedbm.8.xml

libexec_PROGRAMS = makedbm

makedbm_SOURCES = makedbm.c

makedbm_LDADD =  @LIBDBM@  $(top_builddir)/lib/libyp.a @TIRPC_LIBS@

if ENABLE_REGENERATE_MAN
%.8: %.8.xml
	$(XMLLINT) --nonet --xinclude --postvalid --noout $<
	$(XSLTPROC) -o $(srcdir)/$@ --path $(srcdir) --xinclude --nonet http://docbook.sourceforge.net/release/xsl/current/manpages/docbook.xsl $<
endif
