include $(top_srcdir)/buildutils/config.mk

PROG_ROOT = ../..

AM_CFLAGS = -g -DTEST_FUNCTION -I${PROG_ROOT}/ --coverage -DPBS_SERVER_HOME=\"$(PBS_SERVER_HOME)\" -DPBS_ENVIRON=\"$(PBS_ENVIRON)\"

lib_LTLIBRARIES = libpbsd_init.la

AM_LDFLAGS = @CHECK_LIBS@ ${lib_LTLIBRARIES}

check_PROGRAMS = test_pbsd_init

libpbsd_init_la_SOURCES = scaffolding.c ${PROG_ROOT}/pbsd_init.c
libpbsd_init_la_LDFLAGS = @CHECK_LIBS@ -shared -lgcov

test_pbsd_init_LDADD = ../../../test/torque_test_lib/libtorque_test.la ../../../test/scaffold_fail/libscaffold_fail.la
test_pbsd_init_SOURCES = test_pbsd_init.c

check_SCRIPTS = coverage_run.sh

TESTS = ${check_PROGRAMS} coverage_run.sh

coverage_run.sh:
	echo 'cp -p .libs/pbsd_init.gc* . >/dev/null 2>&1' > $@
	echo 'RESULTS=($$(gcov pbsd_init.gcda))' >> $@
	echo 'PARSED_RESULT="TOTALCOV -- $${RESULTS[1]}: Lines($${RESULTS[5]})- $${RESULTS[3]}"' >> $@
	echo 'echo -e "\033[40m\033[1;33m$$PARSED_RESULT\033[0m"' >> $@
	chmod +x $@

CLEANFILES = coverage_run.sh *.gcno *.gcda *.gcov core *.lo
