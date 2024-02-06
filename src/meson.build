
mmidi_sources = files ('''
    setlist.cpp
'''.split())

if host_machine.system() == 'darwin'
    mmidi_sources += 'mmidi.mm'
else
    mmidi_sources += 'mmidi.cpp'
endif

mmidi_ui_type = 'X11UI'
if host_machine.system() == 'windows'
    mmidi_ui_type = 'WindowsUI'
elif host_machine.system() == 'darwin'
    mmidi_ui_type = 'CocoaUI'
endif


plugin = shared_module ('mmidi',
    mmidi_sources,
    name_prefix : '',
    dependencies : [ lvtk_dep ],
    install : true,
    install_dir : lv2_install_dir,
    gnu_symbol_visibility : 'hidden'
)

ui = shared_module ('mmidi-ui',
    'mmidi-ui.cpp',
    name_prefix : '',
    dependencies : [ lvtk_cairo_dep ],
    include_directories : [ '.' ],
    install : true,
    install_dir : lv2_install_dir,
    cpp_args : [ ],
    gnu_symbol_visibility : 'hidden'
)

manifest_ttl = configure_file (
    input : 'manifest.ttl.in',
    output : 'manifest.ttl',
    configuration : {
        'BINARY' : fs.name (plugin.full_path()),
        'UI_BINARY' : fs.name (ui.full_path()),
        'UI_TYPE' : mmidi_ui_type
    },
    install : true,
    install_dir : lv2_install_dir
)

foreach plug : [ 'setlist' ]
    plugin_ttl = configure_file (
        input : 'setlist.ttl.in',
        output : 'setlist.ttl',
        copy : true,
        install : true,
        install_dir : lv2_install_dir
    )

    if lv2_validate.found()
        test ('lv2_validate', lv2_validate, args : [ manifest_ttl, plugin_ttl ])
    endif
endforeach
