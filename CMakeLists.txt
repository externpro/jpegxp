cmake_minimum_required(VERSION 3.0)
project(jpegxp)
include(flags OPTIONAL)
set(lib_name ${PROJECT_NAME})
#######################################
set(include_srcs
  lossy8/jconfig.h
  lossy8/jerror.h
  lossy8/jmorecfg.h
  lossy8/jpeglib.h
  lossy12/xjerror.h
  lossy12/xjpeglib.h
  )
source_group(include FILES ${include_srcs})
list(APPEND ${lib_name}_libsrcs ${include_srcs})
###################
set(internal_hdrs
  lossy8/jchuff.h
  lossy8/jdct.h
  lossy8/jdhuff.h
  lossy8/jinclude.h
  lossy8/jmemsys.h
  lossy8/jpegint.h
  lossy8/jversion.h
  lossy12/xjchuff.h
  lossy12/xjdct.h
  lossy12/xjdhuff.h
  lossy12/xjpegint.h
  lossless/jlossls.h
  )
source_group(headers FILES ${internal_hdrs})
list(APPEND ${lib_name}_libsrcs ${internal_hdrs})
###################
set(lossless_srcs
  lossless/jcodec.c
  lossless/jddiffct.c
  lossless/jdlhuff.c
  lossless/jdlossls.c
  lossless/jdpred.c
  lossless/jdscale.c
  )
source_group(lossless FILES ${lossless_srcs})
list(APPEND ${lib_name}_libsrcs ${lossless_srcs})
###################
set(lossy12_srcs
  lossy12/xjcapimin.c
  lossy12/xjcapistd.c
  lossy12/xjccoefct.c
  lossy12/xjccolor.c
  lossy12/xjcdctmgr.c
  lossy12/xjchuff.c
  lossy12/xjcinit.c
  lossy12/xjcmainct.c
  lossy12/xjcmarker.c
  lossy12/xjcmaster.c
  lossy12/xjcomapi.c
  lossy12/xjcparam.c
  lossy12/xjcphuff.c
  lossy12/xjcprepct.c
  lossy12/xjcsample.c
  lossy12/xjctrans.c
  lossy12/xjdapimin.c
  lossy12/xjdapistd.c
  lossy12/xjdatadst.c
  lossy12/xjdatasrc.c
  lossy12/xjdcoefct.c
  lossy12/xjdcolor.c
  lossy12/xjddctmgr.c
  lossy12/xjdhuff.c
  lossy12/xjdinput.c
  lossy12/xjdmainct.c
  lossy12/xjdmarker.c
  lossy12/xjdmaster.c
  lossy12/xjdmerge.c
  lossy12/xjdphuff.c
  lossy12/xjdpostct.c
  lossy12/xjdsample.c
  lossy12/xjdtrans.c
  lossy12/xjfdctflt.c
  lossy12/xjfdctfst.c
  lossy12/xjfdctint.c
  lossy12/xjidctflt.c
  lossy12/xjidctfst.c
  lossy12/xjidctint.c
  lossy12/xjidctred.c
  lossy12/xjmemmgr.c
  lossy12/xjquant1.c
  lossy12/xjquant2.c
  lossy12/xjutils.c
  )
source_group(lossy12 FILES ${lossy12_srcs})
list(APPEND ${lib_name}_libsrcs ${lossy12_srcs})
###################
set(lossy8_srcs
  lossy8/jcapimin.c
  lossy8/jcapistd.c
  lossy8/jccoefct.c
  lossy8/jccolor.c
  lossy8/jcdctmgr.c
  lossy8/jchuff.c
  lossy8/jcinit.c
  lossy8/jcmainct.c
  lossy8/jcmarker.c
  lossy8/jcmaster.c
  lossy8/jcomapi.c
  lossy8/jcparam.c
  lossy8/jcphuff.c
  lossy8/jcprepct.c
  lossy8/jcsample.c
  lossy8/jctrans.c
  lossy8/jdapimin.c
  lossy8/jdapistd.c
  lossy8/jdatadst.c
  lossy8/jdatasrc.c
  lossy8/jdcoefct.c
  lossy8/jdcolor.c
  lossy8/jddctmgr.c
  lossy8/jdhuff.c
  lossy8/jdinput.c
  lossy8/jdmainct.c
  lossy8/jdmarker.c
  lossy8/jdmaster.c
  lossy8/jdmerge.c
  lossy8/jdphuff.c
  lossy8/jdpostct.c
  lossy8/jdsample.c
  lossy8/jdtrans.c
  lossy8/jerror.c
  lossy8/jfdctflt.c
  lossy8/jfdctfst.c
  lossy8/jfdctint.c
  lossy8/jidctflt.c
  lossy8/jidctfst.c
  lossy8/jidctint.c
  lossy8/jidctred.c
  lossy8/jmemmgr.c
  lossy8/jmemnobs.c
  lossy8/jquant1.c
  lossy8/jquant2.c
  lossy8/jutils.c
  )
source_group(lossy8 FILES ${lossy8_srcs})
list(APPEND ${lib_name}_libsrcs ${lossy8_srcs})
#######################################
if(DEFINED JPEGXP_VER)
  set(ver _${JPEGXP_VER})
  set(verDir /${PROJECT_NAME}${ver})
endif()
#######################################
add_library(${lib_name} STATIC ${${lib_name}_libsrcs})
target_include_directories(${lib_name} PUBLIC $<INSTALL_INTERFACE:$<INSTALL_PREFIX>/include${verDir}>
  PRIVATE lossy8 lossy12 lossless
  )
if(MSVC)
  target_compile_definitions(${lib_name} PRIVATE -D_CRT_SECURE_NO_WARNINGS)
endif()
set_target_properties(${lib_name} PROPERTIES OUTPUT_NAME ${lib_name}${ver})
#######################################
set(targetsFile ${PROJECT_NAME}${ver}-targets)
install(TARGETS ${lib_name} EXPORT ${targetsFile}
  RUNTIME DESTINATION bin
  LIBRARY DESTINATION lib
  ARCHIVE DESTINATION lib
  )
install(FILES ${include_srcs} DESTINATION include${verDir}/${PROJECT_NAME})
if(DEFINED XP_NAMESPACE)
  set(nameSpace NAMESPACE ${XP_NAMESPACE}::)
endif()
install(EXPORT ${targetsFile} DESTINATION lib/cmake ${nameSpace})
