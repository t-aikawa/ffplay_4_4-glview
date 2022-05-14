# ffplay 4.4 on glview

project('ffplay', 'c',
	version: '4.4',
  default_options: ['warning_level=0'])


# glviewのパスを指定してください。
glview = '../glview/'

message('glview project:',glview)

# リンクするopenglを指定する
# gles  :opengles(libglesv2.so)
# opengl:opengl(libOpenGL.so)
opengl_option = get_option('opengl')
if opengl_option == 'gles'
opengl_pkg = 'glesv2'
elif opengl_option == 'opengl'
opengl_pkg = 'OpenGL'
else
opengl_pkg = opengl_option
endif
message('ffplay:select opengl package:',opengl_pkg)

glview_project_path = run_command(
    'cat', files(join_paths(glview,'glview_project.txt')), check: true
).stdout().strip()

cc = meson.get_compiler('c')
dep_libm = cc.find_library('m')
opengl = dependency(opengl_pkg)

libavcodec = dependency('libavcodec')
libavutil = dependency('libavutil')
libswresample = dependency('libswresample')
libavformat = dependency('libavformat')
libswscale = dependency('libswscale')
libavfilter = dependency('libavfilter')
libavdevice = dependency('libavdevice')

SDL2 = dependency('SDL2')

config_include_dir  = join_paths(glview,'builddir',glview_project_path)
glview_include_dir  = join_paths(glview,glview_project_path,'glview')
es1emu_include_dir  = join_paths(glview,glview_project_path,'es1emu')
pthread_include_dir = join_paths(glview,glview_project_path,'pthread')

message('glview include:',glview_include_dir)

includes = include_directories([config_include_dir,glview_include_dir,es1emu_include_dir,pthread_include_dir])
ffplay_includes = include_directories('.')

glview_lib_libdir  = join_paths(meson.current_source_dir() ,glview,'builddir',glview_project_path,'glview')
es1emu_lib_libdir  = join_paths(meson.current_source_dir() ,glview,'builddir',glview_project_path,'es1emu')
pthread_lib_libdir = join_paths(meson.current_source_dir() ,glview,'builddir',glview_project_path,'pthread')

message('glview library:',glview_lib_libdir)

glview_lib = cc.find_library('glview', dirs : glview_lib_libdir)
es1emu_lib = cc.find_library('es1emu', dirs : es1emu_lib_libdir)
pthread_tool_lib = cc.find_library('pthread_tool', dirs : pthread_lib_libdir)

executable(
    'ffplay', [
	'ffplay.c',
	'cmdutils.c'
    ],
    include_directories: [includes,ffplay_includes],  # インクルードディレクトリの指定
	dependencies : [glview_lib,es1emu_lib,pthread_tool_lib,opengl,dep_libm,libavcodec,libavutil,libswresample,libavformat,libswscale,libavfilter,libavdevice,SDL2])
