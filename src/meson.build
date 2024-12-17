libspandsp_sources = files(
    # 'v32bis.c',
    # 'v34rx.c',
    # 'v34tx.c',
    # 'v34_logging.c',
    # 'ssl_fax.c',
    'ademco_contactid.c',
    'adsi.c',
    'agc_float.c',
    'alloc.c',
    'async.c',
    'at_interpreter.c',
    'awgn.c',
    'bell_r2_mf.c',
    'bert.c',
    'bit_operations.c',
    'bitstream.c',
    'complex_filters.c',
    'complex_vector_float.c',
    'complex_vector_int.c',
    'crc.c',
    'data_modems.c',
    'dds_float.c',
    'dds_int.c',
    'dtmf.c',
    'echo.c',
    'fax.c',
    'fax_modems.c',
    'fsk.c',
    'g711.c',
    'g722.c',
    'g726.c',
    'godard.c',
    'gsm0610_decode.c',
    'gsm0610_encode.c',
    'gsm0610_long_term.c',
    'gsm0610_lpc.c',
    'gsm0610_preprocess.c',
    'gsm0610_rpe.c',
    'gsm0610_short_term.c',
    'hdlc.c',
    'ima_adpcm.c',
    'image_translate.c',
    'logging.c',
    'lpc10_analyse.c',
    'lpc10_decode.c',
    'lpc10_encode.c',
    'lpc10_placev.c',
    'lpc10_voicing.c',
    'math_fixed.c',
    'modem_echo.c',
    'modem_connect_tones.c',
    'noise.c',
    'oki_adpcm.c',
    'playout.c',
    'plc.c',
    'power_meter.c',
    'queue.c',
    'schedule.c',
    'sig_tone.c',
    'silence_gen.c',
    'sprt.c',
    'super_tone_rx.c',
    'super_tone_tx.c',
    'swept_tone.c',
    't30.c',
    't30_api.c',
    't30_logging.c',
    't31.c',
    't35.c',
    't38_core.c',
    't38_gateway.c',
    't38_non_ecm_buffer.c',
    't38_terminal.c',
    't4_t6_decode.c',
    't4_t6_encode.c',
    't4_rx.c',
    't4_tx.c',
    't42.c',
    't43.c',
    't81_t82_arith_coding.c',
    't85_decode.c',
    't85_encode.c',
    # 'testcpuid.c',
    'time_scale.c',
    'timezone.c',
    'tone_detect.c',
    'tone_generate.c',
    'v150_1.c',
    'v150_1_sse.c',
    'v17rx.c',
    'v17tx.c',
    'v18.c',
    'v22bis_rx.c',
    'v22bis_tx.c',
    'v27ter_rx.c',
    'v27ter_tx.c',
    'v29rx.c',
    'v29tx.c',
    'v42.c',
    'v42bis.c',
    'v8.c',
    'v80.c',
    'vector_float.c',
    'vector_int.c',
)

if cc.get_define('_MSC_VER') != ''
    libspandsp_sources += files(
        'msvc/gettimeofday.c'
    )
endif

make_incdirs = [include_dirs, include_directories('.')]

if cc.has_define('_MSC_VER')
    make_incdirs += include_directories('msvc')
    getopt = files(
        'msvc/getopt.c'
    )
else
    getopt = []
endif

make_at_dictionary = executable(
    'make_at_dictionary',
    files(
        'make_at_dictionary.c',
    ),
    c_args: ['-DHAVE_CONFIG_H'],
    include_directories: make_incdirs,
    native: true,
    install: false,
)

make_cielab_luts = executable(
    'make_cielab_luts',
    files(
        'make_cielab_luts.c',
    ),
    c_args: ['-DHAVE_CONFIG_H'],
    include_directories: make_incdirs,
    dependencies: m_dep,
    native: true,
    install: false,
)

make_math_fixed_tables = executable(
    'make_math_fixed_tables',
    files(
        'make_math_fixed_tables.c',
    ),
    c_args: ['-DHAVE_CONFIG_H'],
    include_directories: make_incdirs,
    dependencies: m_dep,
    native: true,
    install: false,
)

make_modem_filter = executable(
    'make_modem_filter',
    files(
        'make_modem_filter.c',
        'filter_tools.c',
    ) + getopt,
    c_args: ['-DHAVE_CONFIG_H', '-DSPANDSP_INTERNAL'],
    include_directories: make_incdirs,
    dependencies: m_dep,
    native: true,
    install: false,
)

make_modem_godard_descriptor = executable(
    'make_modem_godard_descriptor',
    files(
        'make_modem_godard_descriptor.c',
        'filter_tools.c',
    ) + getopt,
    c_args: ['-DHAVE_CONFIG_H', '-DSPANDSP_INTERNAL'],
    include_directories: make_incdirs,
    dependencies: m_dep,
    native: true,
    install: false,
)

make_t43_gray_code_tables = executable(
    'make_t43_gray_code_tables',
    files(
        'make_t43_gray_code_tables.c',
    ),
    c_args: ['-DHAVE_CONFIG_H'],
    include_directories: make_incdirs,
    dependencies: m_dep,
    native: true,
    install: false,
)

make_v17_v32_constellation_map = executable(
    'make_v17_v32_constellation_map',
    files(
        'make_v17_v32_constellation_map.c',
        'g711.c',
        'alloc.c',
    ),
    c_args: ['-DHAVE_CONFIG_H', '-DSPANDSP_INTERNAL'],
    include_directories: make_incdirs,
    dependencies: m_dep,
    native: true,
    install: false,
)

make_v17_v32_convolutional_encoder = executable(
    'make_v17_v32_convolutional_encoder',
    files(
        'make_v17_v32_convolutional_encoder.c',
        'g711.c',
        'alloc.c',
    ),
    c_args: ['-DHAVE_CONFIG_H', '-DSPANDSP_INTERNAL'],
    include_directories: make_incdirs,
    dependencies: m_dep,
    native: true,
    install: false,
)

make_v29_constellation_map = executable(
    'make_v29_constellation_map',
    files(
        'make_v29_constellation_map.c',
        'g711.c',
        'alloc.c',
    ),
    c_args: ['-DHAVE_CONFIG_H', '-DSPANDSP_INTERNAL'],
    include_directories: make_incdirs,
    dependencies: m_dep,
    native: true,
    install: false,
)

# make_v34_convolutional_coders = executable(
#     'make_v34_convolutional_coders',
#     files(
#         'make_v34_convolutional_coders.c',
#     ),
#     c_args: ['-DHAVE_CONFIG_H'],
#     include_directories: make_incdirs,
#     dependencies: m_dep,
#     native: true,
#     install: false,
# )

# make_v34_probe_signals = executable(
#     'make_v34_probe_signals',
#     files(
#         'make_v34_probe_signals.c',
#         'g711.c',
#         'alloc.c',
#     ),
#     c_args: ['-DHAVE_CONFIG_H', '-DSPANDSP_INTERNAL'],
#     include_directories: make_incdirs,
#     dependencies: [m_dep, tiff_dep],
#     native: true,
#     install: false,
# )

# make_v34_shell_map = executable(
#     'make_v34_shell_map',
#     files(
#         'make_v34_shell_map.c',
#     ),
#     c_args: ['-DHAVE_CONFIG_H'],
#     include_directories: make_incdirs,
#     native: true,
#     install: false,
# )

# make_v34_tx_pre_emphasis_filters = executable(
#     'make_v34_tx_pre_emphasis_filters',
#     files(
#         'make_v34_tx_pre_emphasis_filters.c',
#         '../tools/meteor-engine.c',
#     ),
#     c_args: ['-DHAVE_CONFIG_H', '-D_USE_MATH_DEFINES'], # M_PI
#     include_directories: make_incdirs + include_directories('../tools'),
#     dependencies: m_dep,
#     native: true,
#     install: false,
# )

at_interpreter_h = custom_target(
    output: 'at_interpreter_dictionary.h',
    capture: true,
    command: [make_at_dictionary]
)

math_fixed_tables_h = custom_target(
    output: 'math_fixed_tables.h',
    capture: true,
    command: [make_math_fixed_tables]
)

cielab_luts_h = custom_target(
    output: 'cielab_luts.h',
    capture: true,
    command: [make_cielab_luts]
)

t43_gray_code_tables_h = custom_target(
    output: 't43_gray_code_tables.h',
    capture: true,
    command: [make_t43_gray_code_tables]
)

v17_v32bis_rx_godard_h = custom_target(
    output: 'v17_v32bis_rx_godard.h',
    capture: true,
    command: [make_modem_godard_descriptor, '1800.0', '2400.0', '0.99', '1000.0', '100.0', '15', '1']
)

v29rx_godard_h = custom_target(
    output: 'v29rx_godard.h',
    capture: true,
    command: [make_modem_godard_descriptor, '1700.0', '2400.0', '0.99', '1000.0', '30.0', '5', '1']
)

# v34_convolutional_coders_h = custom_target(
#     output: 'v34_convolutional_coders.h',
#     capture: true,
#     command: [make_v34_convolutional_coders]
# )

# v34_probe_signals_h = custom_target(
#     output: 'v34_probe_signals.h',
#     capture: true,
#     command: [make_v34_probe_signals]
# )

# v34_shell_map_h = custom_target(
#     output: 'v34_shell_map.h',
#     capture: true,
#     command: [make_v34_shell_map]
# )

# v34_tx_pre_emphasis_filters_h = custom_target(
#     output: 'v34_tx_pre_emphasis_filters.h',
#     capture: false,
#     command: [make_v34_tx_pre_emphasis_filters]
# )

modem_filter_headers = {
    'v17_v32bis_rx_rrc.h': ['-m', 'V.17', '-r'],
    'v17_v32bis_tx_rrc.h': ['-m', 'V.17', '-t'],
    'v22bis_rx_1200_rrc.h': ['-m', 'V.22bis1200', '-r'],
    'v22bis_rx_2400_rrc.h': ['-m', 'V.22bis2400', '-r'],
    'v22bis_tx_rrc.h':  ['-m', 'V.22bis', '-t'],
    'v27ter_rx_2400_rrc.h':  ['-m', 'V.27ter2400', '-r'],
    'v27ter_rx_4800_rrc.h':  ['-m', 'V.27ter4800', '-r'],
    'v27ter_tx_2400_rrc.h':  ['-m', 'V.27ter2400', '-t'],
    'v27ter_tx_4800_rrc.h':  ['-m', 'V.27ter4800', '-t'],
    'v29rx_rrc.h':  ['-m', 'V.29', '-r'],
    'v29tx_rrc.h':  ['-m', 'V.29', '-t'],
    # 'v34_rx_2400_low_carrier_rrc.h': ['-m', 'V.34_2400', '-r'],
    # 'v34_rx_2400_high_carrier_rrc.h': ['-m', 'V.34_2400_high', '-r'],
    # 'v34_rx_2743_low_carrier_rrc.h': ['-m', 'V.34_2743', '-r'],
    # 'v34_rx_2743_high_carrier_rrc.h': ['-m', 'V.34_2743_high', '-r'],
    # 'v34_rx_2800_low_carrier_rrc.h': ['-m', 'V.34_2800', '-r'],
    # 'v34_rx_2800_high_carrier_rrc.h': ['-m', 'V.34_2800_high', '-r'],
    # 'v34_rx_3000_low_carrier_rrc.h': ['-m', 'V.34_3000', '-r'],
    # 'v34_rx_3000_high_carrier_rrc.h': ['-m', 'V.34_3000_high', '-r'],
    # 'v34_rx_3200_low_carrier_rrc.h': ['-m', 'V.34_3200', '-r'],
    # 'v34_rx_3200_high_carrier_rrc.h': ['-m', 'V.34_3200_high', '-r'],
    # 'v34_rx_3429_rrc.h': ['-m', 'V.34_3429', '-r'],
    # 'v34_tx_2400_rrc.h': ['-m', 'V.34_2400', '-t'],
    # 'v34_tx_2743_rrc.h': ['-m', 'V.34_2743', '-t'],
    # 'v34_tx_2800_rrc.h': ['-m', 'V.34_2800', '-t'],
    # 'v34_tx_3000_rrc.h': ['-m', 'V.34_3000', '-t'],
    # 'v34_tx_3200_rrc.h': ['-m', 'V.34_3200', '-t'],
    # 'v34_tx_3429_rrc.h': ['-m', 'V.34_3429', '-t'],
}

foreach k, v : modem_filter_headers
    tgt = custom_target(
        output: [k],
        capture: true,
        command: [make_modem_filter] + v
    )
    libspandsp_sources += [tgt]
endforeach

spandsp_h = configure_file(
    input: 'spandsp.h.in',
    output: 'spandsp.h',
    configuration: inserts,
)

libspandep = both_libraries(
    'spandsp',
    libspandsp_sources + [
        config_h,
        at_interpreter_h,
        math_fixed_tables_h,
        cielab_luts_h,
        t43_gray_code_tables_h,
        v17_v32bis_rx_godard_h,
        v29rx_godard_h,
        # v34_convolutional_coders_h,
        # v34_probe_signals_h,
        # v34_shell_map_h,
        # v34_tx_pre_emphasis_filters_h,
        spandsp_h,
    ] + files(
        'spandsp/version.h',
    ),
    c_args: c_args,
    c_shared_args: c_shared_args,
    dependencies: libs,
    include_directories: make_incdirs,
    version: '3.0.0',
    gnu_symbol_visibility: 'hidden',
    install: true,
)

install_headers(spandsp_h)

install_headers(
    files(
        'spandsp/ademco_contactid.h',
        'spandsp/adsi.h',
        'spandsp/agc_float.h',
        'spandsp/alloc.h',
        'spandsp/async.h',
        'spandsp/arctan2.h',
        'spandsp/at_interpreter.h',
        'spandsp/awgn.h',
        'spandsp/bell_r2_mf.h',
        'spandsp/bert.h',
        'spandsp/biquad.h',
        'spandsp/bit_operations.h',
        'spandsp/bitstream.h',
        'spandsp/crc.h',
        'spandsp/complex.h',
        'spandsp/complex_filters.h',
        'spandsp/complex_vector_float.h',
        'spandsp/complex_vector_int.h',
        'spandsp/data_modems.h',
        'spandsp/dc_restore.h',
        'spandsp/dds.h',
        'spandsp/dtmf.h',
        'spandsp/echo.h',
        'spandsp/fast_convert.h',
        'spandsp/fax.h',
        'spandsp/fax_modems.h',
        'spandsp/fir.h',
        'spandsp/fsk.h',
        'spandsp/g168models.h',
        'spandsp/g711.h',
        'spandsp/g722.h',
        'spandsp/g726.h',
        'spandsp/godard.h',
        'spandsp/gsm0610.h',
        'spandsp/hdlc.h',
        'spandsp/ima_adpcm.h',
        'spandsp/image_translate.h',
        'spandsp/logging.h',
        'spandsp/lpc10.h',
        'spandsp/math_fixed.h',
        'spandsp/modem_echo.h',
        'spandsp/modem_connect_tones.h',
        'spandsp/noise.h',
        'spandsp/oki_adpcm.h',
        'spandsp/playout.h',
        'spandsp/plc.h',
        'spandsp/power_meter.h',
        'spandsp/queue.h',
        'spandsp/saturated.h',
        'spandsp/schedule.h',
        'spandsp/sig_tone.h',
        'spandsp/silence_gen.h',
        'spandsp/sprt.h',
        'spandsp/ssl_fax.h',
        'spandsp/stdbool.h',
        'spandsp/super_tone_rx.h',
        'spandsp/super_tone_tx.h',
        'spandsp/swept_tone.h',
        'spandsp/t30.h',
        'spandsp/t30_api.h',
        'spandsp/t30_fcf.h',
        'spandsp/t30_logging.h',
        'spandsp/t31.h',
        'spandsp/t35.h',
        'spandsp/t38_core.h',
        'spandsp/t38_gateway.h',
        'spandsp/t38_non_ecm_buffer.h',
        'spandsp/t38_terminal.h',
        'spandsp/t4_rx.h',
        'spandsp/t4_tx.h',
        'spandsp/t4_t6_decode.h',
        'spandsp/t4_t6_encode.h',
        'spandsp/t42.h',
        'spandsp/t43.h',
        'spandsp/t81_t82_arith_coding.h',
        'spandsp/t85.h',
        'spandsp/telephony.h',
        'spandsp/time_scale.h',
        'spandsp/timezone.h',
        'spandsp/timing.h',
        'spandsp/tone_detect.h',
        'spandsp/tone_generate.h',
        'spandsp/unaligned.h',
        'spandsp/v150_1.h',
        'spandsp/v150_1_sse.h',
        'spandsp/v17rx.h',
        'spandsp/v17tx.h',
        'spandsp/v18.h',
        'spandsp/v22bis.h',
        'spandsp/v27ter_rx.h',
        'spandsp/v27ter_tx.h',
        'spandsp/v29rx.h',
        'spandsp/v29tx.h',
        # 'spandsp/v32bis.h',
        # 'spandsp/v34.h',
        'spandsp/v42.h',
        'spandsp/v42bis.h',
        'spandsp/v8.h',
        'spandsp/v80.h',
        'spandsp/vector_float.h',
        'spandsp/vector_int.h',
        'spandsp/version.h',
        'spandsp/private/ademco_contactid.h',
        'spandsp/private/adsi.h',
        'spandsp/private/agc_float.h',
        'spandsp/private/async.h',
        'spandsp/private/at_interpreter.h',
        'spandsp/private/awgn.h',
        'spandsp/private/bell_r2_mf.h',
        'spandsp/private/bert.h',
        'spandsp/private/bitstream.h',
        'spandsp/private/data_modems.h',
        'spandsp/private/dtmf.h',
        'spandsp/private/echo.h',
        'spandsp/private/fax.h',
        'spandsp/private/fax_modems.h',
        'spandsp/private/fsk.h',
        'spandsp/private/g711.h',
        'spandsp/private/g722.h',
        'spandsp/private/g726.h',
        'spandsp/private/godard.h',
        'spandsp/private/gsm0610.h',
        'spandsp/private/hdlc.h',
        'spandsp/private/ima_adpcm.h',
        'spandsp/private/image_translate.h',
        'spandsp/private/logging.h',
        'spandsp/private/lpc10.h',
        'spandsp/private/modem_connect_tones.h',
        'spandsp/private/modem_echo.h',
        'spandsp/private/noise.h',
        'spandsp/private/oki_adpcm.h',
        'spandsp/private/playout.h',
        'spandsp/private/plc.h',
        'spandsp/private/power_meter.h',
        'spandsp/private/queue.h',
        'spandsp/private/schedule.h',
        'spandsp/private/sig_tone.h',
        'spandsp/private/silence_gen.h',
        'spandsp/private/sprt.h',
        # 'spandsp/private/ssl_fax.h',
        'spandsp/private/super_tone_rx.h',
        'spandsp/private/super_tone_tx.h',
        'spandsp/private/swept_tone.h',
        'spandsp/private/t30.h',
        'spandsp/private/t30_dis_dtc_dcs_bits.h',
        'spandsp/private/t31.h',
        'spandsp/private/t38_core.h',
        'spandsp/private/t38_gateway.h',
        'spandsp/private/t38_non_ecm_buffer.h',
        'spandsp/private/t38_terminal.h',
        'spandsp/private/t4_rx.h',
        'spandsp/private/t4_tx.h',
        'spandsp/private/t4_t6_decode.h',
        'spandsp/private/t4_t6_encode.h',
        'spandsp/private/t42.h',
        'spandsp/private/t43.h',
        'spandsp/private/t81_t82_arith_coding.h',
        'spandsp/private/t85.h',
        'spandsp/private/time_scale.h',
        'spandsp/private/timezone.h',
        'spandsp/private/tone_detect.h',
        'spandsp/private/tone_generate.h',
        'spandsp/private/v150_1.h',
        'spandsp/private/v150_1_sse.h',
        'spandsp/private/v17rx.h',
        'spandsp/private/v17tx.h',
        'spandsp/private/v18.h',
        'spandsp/private/v22bis.h',
        'spandsp/private/v27ter_rx.h',
        'spandsp/private/v27ter_tx.h',
        'spandsp/private/v29rx.h',
        'spandsp/private/v29tx.h',
        # 'spandsp/private/v32bis.h',
        # 'spandsp/private/v34.h',
        'spandsp/private/v42.h',
        'spandsp/private/v42bis.h',
        'spandsp/private/v8.h',
        'spandsp/private/v80.h',
        'spandsp/expose.h',
    ),
    preserve_path : true
)
