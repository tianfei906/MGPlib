## This is a automake file, part of Unidata's netCDF package.
# Copyright 2005, see the COPYRIGHT file for more information.
# This file builds and runs the ncdump program.

# $Id: Makefile.am,v 1.147 2010/05/29 00:50:39 dmh Exp $

# Put together AM_CPPFLAGS and AM_LDFLAGS.
include $(top_srcdir)/lib_flags.am
LDADD = ${top_builddir}/liblib/libnetcdf.la

TESTS_ENVIRONMENT=CC=${CC}

# This is the program we're building, and it's sources.
bin_PROGRAMS = ncdump
ncdump_SOURCES = ncdump.c vardata.c dumplib.c indent.c nctime0.c	\
ncdump.h vardata.h dumplib.h indent.h isnan.h nctime0.h cdl.h \
utils.h utils.c nciter.h nciter.c nccomps.h

# Another utility program that copies any netCDF file using only the
# netCDF API
bin_PROGRAMS += nccopy
nccopy_SOURCES = nccopy.c nciter.c nciter.h chunkspec.h chunkspec.c \
utils.h utils.c dimmap.h dimmap.c

# This is the man page.
man_MANS = ncdump.1 nccopy.1

if BUILD_TESTSETS
#if !BUILD_DLL
# These tests are run for both netCDF-4 and non-netCDF-4 builds.
check_PROGRAMS = rewrite-scalar ctest ctest64 ncdump tst_utf8 bom
TESTS = run_tests.sh tst_64bit.sh ctest ctest64 tst_output.sh	\
tst_lengths.sh tst_calendars.sh tst_utf8 run_utf8_tests.sh      \
tst_nccopy3.sh tst_charfill.sh tst_iter.sh tst_formatx3.sh tst_bom.sh

if LARGE_FILE_TESTS
TESTS += tst_iter.sh
endif

if USE_NETCDF4
# NetCDF-4 has some extra tests.
check_PROGRAMS += tst_create_files tst_h_rdc0 tst_group_data		\
tst_enum_data tst_opaque_data tst_string_data tst_vlen_data tst_comp	\
tst_comp2 tst_nans tst_special_atts tst_unicode tst_fillbug tst_compress \
tst_chunking tst_h_scalar tst_bug324

TESTS += tst_create_files tst_group_data tst_enum_data tst_opaque_data	\
tst_string_data tst_vlen_data tst_comp tst_comp2 tst_nans		\
tst_special_atts tst_netcdf4.sh tst_h_rdc0 tst_unicode tst_fillbug	\
tst_fillbug.sh tst_netcdf4_4.sh tst_compress tst_nccopy4.sh             \
tst_grp_spec.sh tst_mud.sh tst_h_scalar tst_h_scalar.sh tst_formatx4.sh \
tst_bug324

if EXTRA_TESTS
TESTS += run_back_comp_tests.sh
endif # EXTRA_TESTS

tst_h_rdc0_CPPFLAGS = -I${top_srcdir}/nc_test ${AM_CPPFLAGS}

endif #!USE_NETCDF4
#endif #!BUILD_DLL

# Can't run ncgen to generate ctest.c and ctest64.c on cross-compiles.
BUILT_SOURCES = ctest.c ctest64.c
if EXTRA_TESTS
ctest.c:
	$(top_builddir)/ncgen/ncgen -lc -o ctest0.nc $(top_srcdir)/ncgen/c0.cdl >$(srcdir)/ctest.c

ctest64.c:
	$(top_builddir)/ncgen/ncgen -v2 -lc -o ctest0_64.nc $(top_srcdir)/ncgen/c0.cdl > $(srcdir)/ctest64.c
else
ctest.c:
	cp $(top_srcdir)/ncdump/ref_ctest.c $(top_srcdir)/ncdump/ctest.c

ctest64.c:
	cp $(top_srcdir)/ncdump/ref_ctest64.c $(top_srcdir)/ncdump/ctest64.c
endif

#if !BUILD_DLL
TESTS += tst_ncgen4_classic.sh
if USE_NETCDF4
TESTS += tst_ncgen4.sh
endif
#endif

endif BUILD_TESTSETS

CLEANFILES = test0.nc test1.cdl test1.nc test2.cdl ctest1.cdl	\
ctest0.nc ctest0_64.nc c1.cdl c1_4.cdl ctest1_64.cdl c0.nc c0_4.nc small.nc	\
small2.nc c0tmp.nc c1.ncml utf8.cdl utf8_64.cdl utf8.nc utf8_64.nc	\
tmp.cdl tst_vlen_data.nc tst_utf8.nc tst_special_atts.nc		\
tst_unicode.nc tst_solar_2.nc tst_string_data.nc tst_calendars.nc	\
tst_nans.nc tst_opaque_data.nc tst_solar_cmp.nc tst_enum_data.nc	\
tst_solar_1.nc tst_mslp_64.nc tst_mslp.nc tst_bug321.nc tst_comp2.nc tst_ncml.nc	\
tst_fillbug.nc tst_group_data.nc tst_small.nc tst_comp.nc		\
tst_unicode.cdl tst_group_data.cdl tst_compounds2.cdl tst_comp.cdl	\
tst_enum_data.cdl tst_small.cdl tst_times.cdl tst_solar_2.cdl		\
tst_string_data.cdl tst_fillbug.cdl tst_opaque_data.cdl			\
tst_compounds4.cdl tst_utf8.cdl tst_compounds3.cdl			\
tst_special_atts.cdl tst_nans.cdl tst_format_att_64.cdl			\
tst_vlen_data.cdl tst_solar_1.cdl tst_format_att.cdl tst_inflated.nc    \
tmp_subset.cdl tst_inflated4.nc tst_deflated.nc tst_chunking.nc tmp*.nc \
tst_charfill.nc tmp_tst_charfill.cdl \
iter.* \
tst_nc_test_netcdf4_4_0.cdl tst_mud4.nc tst_mud4.cdl tst_mud4-bc.cdl \
tst_ncf213.cdl tst_ncf213.nc tst_h_scalar.cdl tst_h_scalar.nc \
tst_mud4_chars.cdl tst_mud4_chars.nc

# These files all have to be included with the distribution.
EXTRA_DIST = run_tests.sh tst_64bit.sh tst_output.sh test0.cdl		\
ref_ctest1_nc4.cdl ref_ctest1_nc4c.cdl ref_tst_solar_1.cdl		\
ref_tst_solar_2.cdl tst_netcdf4.sh tst_netcdf4_4.sh ref_tst_small.cdl	\
tst_lengths.sh tst_ncml.cdl ref1.ncml ref_tst_group_data.cdl		\
ref_tst_enum_data.cdl ref_tst_opaque_data.cdl ref_tst_string_data.cdl	\
ref_tst_vlen_data.cdl ref_tst_comp.cdl ref_tst_unicode.cdl		\
ref_tst_nans.cdl small.cdl small2.cdl $(man_MANS) run_utf8_tests.sh	\
ref_tst_utf8.cdl ref_tst_fillbug.cdl tst_fillbug.sh tst_calendars.cdl	\
tst_calendars.sh ref_times.cdl ref_tst_special_atts.cdl			\
ref_tst_noncoord.cdl ref_tst_compounds2.nc ref_tst_compounds2.cdl	\
ref_tst_compounds3.nc ref_tst_compounds3.cdl ref_tst_compounds4.nc	\
ref_tst_compounds4.cdl ref_tst_group_data_v23.cdl tst_mslp.cdl tst_bug321.cdl \
ref_tst_format_att.cdl ref_tst_format_att_64.cdl tst_nccopy3.sh		\
tst_nccopy4.sh ref_nc_test_netcdf4_4_0.nc run_back_comp_tests.sh	\
ref_nc_test_netcdf4.cdl ref_tst_special_atts3.cdl tst_brecs.cdl         \
ref_tst_grp_spec0.cdl ref_tst_grp_spec.cdl tst_grp_spec.sh              \
ref_tst_charfill.cdl tst_charfill.cdl tst_charfill.sh                   \
tst_iter.sh tst_mud.sh ref_tst_mud4.cdl ref_tst_mud4-bc.cdl             \
ref_tst_mud4_chars.cdl \
ref_tst_ncf213.cdl tst_h_scalar.sh                                      \
tst_formatx3.sh tst_formatx4.sh                                         \
CMakeLists.txt XGetopt.c tst_bom.sh

# CDL files and Expected results
SUBDIRS=cdl expected
EXTRA_DIST += tst_ncgen_shared.sh tst_ncgen4.sh tst_ncgen4_classic.sh	\
tst_ncgen4_diff.sh tst_ncgen4_cycle.sh ref_ctest.c ref_ctest64.c \
ctest.c ctest64.c

CLEANFILES += results/*.nc results/*.dmp results/*.dmp2 tmp*.cdl tst_bug324.nc
DISTCLEANFILES = results
