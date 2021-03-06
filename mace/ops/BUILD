# Description:
# Mace operators.
#
package(
    default_visibility = ["//visibility:public"],
)

licenses(["notice"])  # Apache 2.0

load(
    "//mace:mace.bzl",
    "if_android",
    "if_neon_enabled",
    "if_openmp_enabled",
    "if_android_armv7",
    "if_hexagon_enabled",
    "if_opencl_enabled",
)

cc_library(
    name = "test",
    testonly = 1,
    hdrs = glob([
        "*_test_util.h",
    ]),
    srcs = [
        "ops_test_util.cc",
    ],
    copts = [
        "-Werror",
        "-Wextra",
    ] + if_openmp_enabled(["-fopenmp"]) + if_neon_enabled([
        "-DMACE_ENABLE_NEON",
    ]) + if_android_armv7([
        "-mfpu=neon",
    ]) + if_android_armv7([
        "-mfloat-abi=softfp",
    ]) + if_opencl_enabled([
        "-DMACE_ENABLE_OPENCL",
    ]) + if_hexagon_enabled([
        "-DMACE_ENABLE_HEXAGON",
    ]),
    deps = [
        "//mace/ops",
        "@gtest",
    ],
)

cc_library(
    name = "ops",
    srcs = glob(
        ["*.cc"],
        exclude = [
            "*_test.cc",
            "*_benchmark.cc",
            "ops_test_util.cc",
            "buffer_to_image.cc",
            "image_to_buffer.cc",
            "lstmcell.cc",
        ],
    ) + if_opencl_enabled(
        [
            "buffer_to_image.cc",
            "image_to_buffer.cc",
            "lstmcell.cc",
        ],
    ),
    hdrs = glob(
        ["*.h"],
        exclude = glob(["*_test_util.h"]),
    ),
    copts = [
        "-Werror",
        "-Wextra",
    ] + if_openmp_enabled(["-fopenmp"]) + if_neon_enabled([
        "-DMACE_ENABLE_NEON",
    ]) + if_android_armv7([
        "-mfpu=neon",
    ]) + if_android_armv7([
        "-mfloat-abi=softfp",
    ]) + if_opencl_enabled([
        "-DMACE_ENABLE_OPENCL",
    ]) + if_hexagon_enabled([
        "-DMACE_ENABLE_HEXAGON",
    ]),
    deps = [
        "//mace/kernels",
    ],
)

cc_test(
    name = "ops_test",
    testonly = 1,
    srcs = glob(
        ["*_test.cc"],
    ),
    copts = [
        "-Werror",
        "-Wextra",
    ] + if_openmp_enabled(["-fopenmp"]) + if_neon_enabled([
        "-DMACE_ENABLE_NEON",
    ]) + if_android_armv7([
        "-mfpu=neon",
    ]) + if_android_armv7([
        "-mfloat-abi=softfp",
    ]) + if_opencl_enabled([
        "-DMACE_ENABLE_OPENCL",
    ]) + if_hexagon_enabled([
        "-DMACE_ENABLE_HEXAGON",
    ]),
    linkopts = ["-fopenmp"],
    linkstatic = 1,
    deps = [
        ":ops",
        ":test",
        "@gtest//:gtest_main",
    ],
)

cc_test(
    name = "ops_benchmark",
    testonly = 1,
    srcs = glob(["*_benchmark.cc"]),
    copts = [
        "-Werror",
        "-Wextra",
    ] + if_openmp_enabled(["-fopenmp"]) + if_neon_enabled([
        "-DMACE_ENABLE_NEON",
    ]) + if_android_armv7([
        "-mfpu=neon",
    ]) + if_android_armv7([
        "-mfloat-abi=softfp",
    ]) + if_opencl_enabled([
        "-DMACE_ENABLE_OPENCL",
    ]) + if_hexagon_enabled([
        "-DMACE_ENABLE_HEXAGON",
    ]),
    linkopts = ["-fopenmp"],
    linkstatic = 1,
    deps = [
        ":ops",
        ":test",
        "//mace/core:test_benchmark_main",
    ],
)
