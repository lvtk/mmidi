# LV2 installation directory.
lv2_install_dir = get_option ('lv2dir').strip()
if lv2_install_dir != ''
    lv2_install_dir = fs.expanduser (lv2_install_dir)
endif

if lv2_install_dir == ''
    if target_machine.system() == 'darwin'
        lv2_install_dir = fs.expanduser ('~/Library/Audio/Plug-Ins/LV2')
    elif target_machine.system() == 'haiku'
        lv2_install_dir = '/boot/common/add-ons/lv2'
    elif target_machine.system() == 'windows'
        lv2_install_dir = fs.expanduser ('~/AppData/Roaming/LV2')
    else
        lv2_install_dir = fs.expanduser('~/.lv2')
    endif
endif

# Add objective-c if on mac
if host_machine.system() == 'darwin'
  add_languages(['objc', 'objcpp'], native : false, required : true)
  objcc = meson.get_compiler ('objc')
  objcpp = meson.get_compiler ('objcpp')
endif

# Evaluation tools
lv2_validate = find_program ('lv2_validate', required : false)

if not meson.is_subproject()
    add_global_arguments (['-DLVTK_STATIC=1', '-DPUGL_STATIC=1'],
        language : [ 'c', 'cpp' ])
endif

# LVTK Setup
lvtk_opts = [
    'doc=disabled',
    'test=disabled',
    'demo=disabled',
    'default_library=static'
]

lvtk_dep = dependency ('lvtk-3', 
    fallback : [ 'lvtk', 'lvtk_dep' ],
    version : '>= 3.0.0',
    default_options : lvtk_opts,
    required : true
)

lvtk_cairo_dep = dependency ('lvtk-cairo-3', 
    fallback : [ 'lvtk', 'lvtk_cairo_dep' ],
    version : '>= 3.0.0',
    default_options : lvtk_opts,
    required : true
)
