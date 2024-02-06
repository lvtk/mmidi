project ('mmidi', ['c', 'cpp'],
    version : '1.0.0',
    default_options : [ 
        'cpp_std=c++17', 
        'default_library=static',
        'b_ndebug=if-release',
        'buildtype=release',
        'c_std=c99',
    ])

fs = import ('fs')

subdir('meson/lvtk-cairo')

lv2_bundle = 'mmidi.lv2'
lv2_install_dir = lv2_install_dir / lv2_bundle

subdir ('src')

summary ('Install', lv2_install_dir, section : 'LV2')
