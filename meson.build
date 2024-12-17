project('spandsp', 'c',
    version: '0.0.6',
    meson_version: '>= 1.3.0',
    default_options: [
        'buildtype=debugoptimized',
        'c_std=gnu11,c11'
    ]
)

cc = meson.get_compiler('c')

c_args = [
    '-DHAVE_CONFIG_H',
]

if cc.get_define('_MSC_VER') != ''
    c_args += [
        '-D_USE_MATH_DEFINES', # M_PI
        '-D_CRT_SECURE_NO_DEPRECATE',
        '-D_CRT_NONSTDC_NO_DEPRECATE',
        '-D_CRT_SECURE_NO_WARNINGS', # sprintf, sscanf,
    ]
endif

conf = configuration_data()
inserts = configuration_data()

libtiff_dep = dependency('libtiff-4', required: true)

conf.set('__inline__', 'inline')

if not cc.has_function('lrint', prefix: '#include <math.h>') and not cc.has_function('lrintf', prefix: '#include <math.h>')
    warning('Missing C99 standard functions lrint() and lrintf().\nThis may cause benign compiler warnings on some systems (ie Solaris).')
endif

# MSVC does not complain if a function's missing until link time
conf.set('HAVE_ALIGNED_ALLOC', cc.links('''#define _ISOC11_SOURCE
#include <stdlib.h>
int main() { aligned_alloc(0,0); return 0; }
''', name: 'Supports aligned_alloc'))

symbols = [
    'memalign',
    'memmove',
    'memset',
    'select',
    'strcasecmp',
    'strchr',
    'strdup',
    'strerror',
    'strstr',
    'strtol',
    'gettimeofday',
    'drand48',
]

foreach f: symbols
    conf.set('HAVE_@0@'.format(f.to_upper()), cc.has_function(f))
endforeach

# https://github.com/mesonbuild/meson/issues/1083
conf.set('HAVE_POSIX_MEMALIGN', cc.has_function('posix_memalign', prefix: '#include <stdlib.h>'))

headers = [
    'socket.h',
    'inttypes.h',
    'stdint.h',
    'stdbool.h',
    'stdfix.h',
    'unistd.h',
    'stdlib.h',
    'string.h',
    'strings.h',
    'malloc.h',
    'math.h',
    'float.h',
    'fcntl.h',
    'sys/time.h',
    # 'sys/select.h',
    # 'sys/ioctl.h',
    'sys/fcntl.h',
    # 'sndfile.h',
    # 'fenv.h',
    # 'fftw3.h',
    # 'fftw.h',
    # 'pcap.h',
    # 'pthread.h',
    'getopt.h',
]

if host_machine.system() not in ['dragonfly', 'netbsd', 'freebsd']
    headers += ['tgmath.h']
endif

# MSVC needs /experimental:c11atomics
if cc.compiles('#include <stdatomic.h>\nint main() {return 0;}', name: 'Supports C11 atomics')
    conf.set('HAVE_STDATOMIC_H', 1)
endif

foreach h: headers
    conf.set('HAVE_@0@'.format(h.underscorify().to_upper()), cc.has_header(h))
endforeach

include_these_headers = [
    'inttypes.h',
    'stdint.h',
    'stdbool.h',
    'math.h',
]
foreach h: headers
    id = h.underscorify().to_upper()
    k = id.replace('_H', '_HEADER')
    if conf.get('HAVE_@0@'.format(id))
        inserts.set('INSERT_@0@'.format(k), '#include <@0@>'.format(h))
    endif
endforeach

libxml_dep = dependency('libxml-2.0', required: false)

if libxml_dep.found()
    headers = [
        'libxml/xmlmemory.h',
        'libxml/parser.h',
        'libxml/xinclude.h',
    ]

    foreach h: headers
        conf.set('HAVE_@0@'.format(h.underscorify().to_upper()), cc.has_header(h, dependencies: libxml_dep))
    endforeach
endif

# FIXME: fltk support is for tests only, needs C++ and CMake support
# See https://www.fltk.org/str.php?L2180

m_dep = cc.find_library('m', required: false)

conf.set('HAVE_OPEN_MEMSTREAM', cc.has_function('open_memstream', dependencies: m_dep))

cc.has_function('cos', dependencies: m_dep, required: true)

symbols = [
    'sinf',
    'cosf',
    'tanf',
    'asinf',
    'acosf',
    'atanf',
    'atan2f',
    'ceilf',
    'floorf',
    'powf',
    'expf',
    'logf',
    'log10f',
]

foreach f: symbols
    conf.set('HAVE_@0@'.format(f.to_upper()), cc.has_function(f, dependencies: m_dep))
endforeach

c_shared_args = []
if host_machine.system() in ['windows', 'cygwin']
    c_shared_args += ['-DLIBSPANDSP_EXPORTS', '-DSPANDSP_USE_EXPORT_CAPABILITY']
    inserts.set('SPANDSP_USE_EXPORT_CAPABILITY', '#define SPANDSP_USE_EXPORT_CAPABILITY 1')
elif cc.has_function_attribute('visibility:default')
    c_args += ['-DSPANDSP_USE_EXPORT_CAPABILITY']
    inserts.set('SPANDSP_USE_EXPORT_CAPABILITY', '#define SPANDSP_USE_EXPORT_CAPABILITY 1')
else
    # conf.set('SPANDSP_USE_EXPORT_CAPABILITY', false)
    inserts.set('SPANDSP_USE_EXPORT_CAPABILITY', '#undef SPANDSP_USE_EXPORT_CAPABILITY')
endif

c_args += cc.get_supported_arguments([
    '-ffast-math',
    '/fp:fast',
    '-Wunused-variable',
    '-Wwrite-strings',
    '-Wstrict-prototypes',
    '-Wmissing-prototypes',
    '-Wunused-but-set-variable',
    '/wd4100', # The formal parameter is not referenced in the body of the function. The unreferenced parameter is ignored.
    '/wd4200', # Non standard extension C zero sized array
    '/wd4706', # assignment within conditional expression
    '/wd4244', # conversion from 'type1' to 'type2', possible loss of data
    '/wd4295', # array is too small to include a terminating null character
    '/wd4125', # decimal digit terminates octal escape sequence
    '/wd4305', # 'function' : truncation from 'double' to 'float'
    '/wd4018', # '<' : signed/unsigned mismatch
    '/wd4389', # '==' : signed/unsigned mismatch
    '/wd4285', # 'return' : conversion from 'int' to 'size_t', signed/unsigned mismatch
    '/wd4267', # '=': conversion from 'size_t' to 'int', possible loss of data
    '/wd4005', # '__inline__': macro redefinition
])

# We do not activate instruction sets here as this library has no cpuid capability
if cc.has_define('_MSC_VER')
    inserts.set('SPANDSP_USE_FIXED_POINT', '#ifdef _MSC_VER\n#define __inline__ __inline\n#pragma warning(disable:4200)\n#endif\n#undef SPANDSP_USE_FIXED_POINT')
else
    inserts.set('SPANDSP_USE_FIXED_POINT', '#undef SPANDSP_USE_FIXED_POINT')
endif
if host_machine.cpu_family() != 'arm'
    conf.set('SPANDSP_MISALIGNED_ACCESS_FAILS', true)
    inserts.set('SPANDSP_MISALIGNED_ACCESS_FAILS', '#define SPANDSP_MISALIGNED_ACCESS_FAILS 1')
else
    inserts.set('SPANDSP_MISALIGNED_ACCESS_FAILS', '#undef SPANDSP_MISALIGNED_ACCESS_FAILS')
endif

sets = {
    '__AVX__': 'SPANDSP_USE_AVX',
    '__SSE4_2__': 'SPANDSP_USE_SSE4_2',
    '__SSE4_1__': 'SPANDSP_USE_SSE4_1',
    '__SSSE3__': 'SPANDSP_USE_SSSE3',
    '__SSE3__': 'SPANDSP_USE_SSE3',
    '__SSE2__': 'SPANDSP_USE_SSE2',
    '__SSE__': 'SPANDSP_USE_SSE',
    '__MMX__': 'SPANDSP_USE_MMX',
}
enable_all_arches = false
# FIXME: MSVC provides no way to detect /arch:SSE4.2
if cc.get_define('_M_IX86_FP') == '2' or cc.has_define('__AVX2__')
    enable_all_arches = true
elif cc.get_define('_M_IX86_FP') == '1' or (cc.get_argument_syntax() == 'msvc' and host_machine.cpu_family() == 'x86_64')
    enable_all_arches = true
    sets = {
        '__SSE2__': 'SPANDSP_USE_SSE2',
        '__SSE__': 'SPANDSP_USE_SSE',
        '__MMX__': 'SPANDSP_USE_MMX',
    }
endif
foreach k, v : sets
    if enable_all_arches or cc.has_define(k)
        conf.set(v, 1)
    endif
endforeach

tiff_dep = dependency('libtiff-4')

if cc.has_function('TIFFCreateCustomDirectory', dependencies: tiff_dep)
    if cc.has_header('tif_dir.h', dependencies: tiff_dep)
        conf.set('SPANDSP_SUPPORT_TIFF_FX', 1)
        inserts.set('SPANDSP_SUPPORT_TIFF_FX', '#define SPANDSP_SUPPORT_TIFF_FX 1')
    else
        inserts.set('SPANDSP_SUPPORT_TIFF_FX', '#undef SPANDSP_SUPPORT_TIFF_FX')
    endif
    conf.set('SPANDSP_SUPPORT_T43', 1)
    inserts.set('SPANDSP_SUPPORT_T43', '#define SPANDSP_SUPPORT_T43 1')
else
    inserts.set('SPANDSP_SUPPORT_TIFF_FX', '#undef SPANDSP_SUPPORT_TIFF_FX')
    inserts.set('SPANDSP_SUPPORT_T43', '#undef SPANDSP_SUPPORT_T43')
endif

jpeg_dep = dependency('libjpeg')

# ssl_dep = cc.find_library('ssl', required: false)

# conf.set('SPANDSP_SUPPORT_FLEXSSL', cc.has_function('TLS_client_method', dependencies: ssl_dep))

winsock_dep = cc.find_library('ws2_32', required: false)

libs = [m_dep, tiff_dep, jpeg_dep, winsock_dep] #, ssl_dep]

# conf.set('SPANDSP_SUPPORT_V32BIS', 1)
# inserts.set('SPANDSP_SUPPORT_V32BIS', '#define SPANDSP_SUPPORT_V32BIS 1')
inserts.set('SPANDSP_SUPPORT_V32BIS', '#undef SPANDSP_SUPPORT_V32BIS')
# conf.set('SPANDSP_SUPPORT_V34', 1)
# inserts.set('SPANDSP_SUPPORT_V34', '#define SPANDSP_SUPPORT_V34 1')
inserts.set('SPANDSP_SUPPORT_V34', '#undef SPANDSP_SUPPORT_V34')
# conf.set('SPANDSP_SUPPORT_SSLFAX', 1)

conf.set_quoted('PACKAGE', meson.project_name())
conf.set_quoted('VERSION', meson.project_version())

config_h = configure_file(
    output: 'config.h',
    configuration: conf
)

include_dirs = include_directories('.')

subdir('src')

pkg = import('pkgconfig')

pkg.generate(
    libspandep,
    description: 'A DSP library for telephony.',
)
