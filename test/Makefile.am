check_SCRIPTS=run-test.sh
TEST_EXTENSIONS = \
	.sh \
	$(NULL)

AM_TESTS_ENVIRONMENT= \
	src=${srcdir}; export src; \
	EXEEXT=${EXEEXT}; export EXEEXT; \
	$(NULL)

BUILT_SOURCES = $(builddir)/out.expected

SH_LOG_COMPILER = sh
TESTS=run-test.sh

TESTDATA=4x6.pcf 8x16.pcf fonts.conf.in

if FREETYPE_PCF_LONG_FAMILY_NAMES
$(builddir)/out.expected: $(srcdir)/out.expected-long-family-names Makefile
	cp $(srcdir)/out.expected-long-family-names $(builddir)/out.expected
else
$(builddir)/out.expected: $(srcdir)/out.expected-no-long-family-names Makefile
	cp $(srcdir)/out.expected-no-long-family-names $(builddir)/out.expected
endif

AM_CPPFLAGS = -I$(top_srcdir) -I$(top_builddir)

check_PROGRAMS =
if HAVE_PTHREAD
check_PROGRAMS += test-pthread
test_pthread_LDADD = $(top_builddir)/src/libfontconfig.la
# We don't enable this test by default because it will require config and fonts
# to meaningfully test anything, and we are not installed yet.
#TESTS += test-pthread
endif
check_PROGRAMS += test-bz89617
test_bz89617_CFLAGS = \
	-DSRCDIR="\"$(abs_srcdir)\""

test_bz89617_LDADD = $(top_builddir)/src/libfontconfig.la
TESTS += test-bz89617

check_PROGRAMS += test-bz131804
test_bz131804_LDADD = $(top_builddir)/src/libfontconfig.la
TESTS += test-bz131804

noinst_PROGRAMS = $(check_PROGRAMS)

if !OS_WIN32
check_PROGRAMS += test-migration
test_migration_LDADD = $(top_builddir)/src/libfontconfig.la
endif

check_PROGRAMS += test-bz96676
test_bz96676_LDADD = $(top_builddir)/src/libfontconfig.la
TESTS += test-bz96676

check_PROGRAMS += test-name-parse
test_name_parse_LDADD = $(top_builddir)/src/libfontconfig.la
TESTS += test-name-parse

EXTRA_DIST=run-test.sh $(TESTDATA) out.expected-long-family-names out.expected-no-long-family-names

CLEANFILES=out fonts.conf out.expected

-include $(top_srcdir)/git.mk
