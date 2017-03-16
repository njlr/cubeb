MACOS_CUBEB_STDINT_H = """
#ifndef _LIBCUBEB_INCLUDE_CUBEB_CUBEB_STDINT_H
#define _LIBCUBEB_INCLUDE_CUBEB_CUBEB_STDINT_H 1
#ifndef _GENERATED_STDINT_H
#define _GENERATED_STDINT_H \\"libcubeb 0.2\\"
/* generated using gnu compiler Apple LLVM version 8.0.0 (clang-800.0.42.1) */
#define _STDINT_HAVE_STDINT_H 1
#include <stdint.h>
#endif
#endif
"""

genrule(
  name = 'macos-cubeb-stdint.h',
  out = 'cubeb-stdint.h',
  cmd = 'echo "' + MACOS_CUBEB_STDINT_H + '" > $OUT',
)

macos_exported_headers = {
  'cubeb-stdint.h': ':macos-cubeb-stdint.h',
}

macos_exported_linker_flags = [
  '-framework', 'CoreServices',
  '-framework', 'AudioUnit',
]

cxx_library(
  name = 'cubeb',
  header_namespace = 'cubeb',
  exported_headers = subdir_glob([
    ('include/cubeb', '*.h'),
  ]),
  exported_platform_headers = [
    ('default', macos_exported_headers),
    ('^macos.*', macos_exported_headers),
  ],
  platform_srcs = [
    ('default', ['src/cubeb_audiounit.c']),
    ('^macos.*', ['src/cubeb_audiounit.c']),
    ('^windows.*', ['src/cubeb_directsound.cpp']),
  ],
  exported_platform_linker_flags = [
    ('default', macos_exported_linker_flags),
    ('^macos.*', macos_exported_linker_flags),
  ],
  visibility = [
    'PUBLIC',
  ],
)
