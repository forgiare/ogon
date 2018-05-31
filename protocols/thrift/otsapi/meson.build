generated_ots_thrift = custom_target('gen-thrift-ots',
       input: '../otsapi.thrift',
       output: ['@BASENAME@_types.cpp', '@BASENAME@_types.h',
			 '@BASENAME@.cpp', '@BASENAME@.h'],
       command: [thrift, '--gen', 'cpp', '-out', '@OUTDIR@', '@INPUT@'],
)

includes_generated_ots = include_directories('..')
