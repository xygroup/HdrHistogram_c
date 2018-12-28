cc_library(
    name = "hdr_histogram",
    hdrs = glob(["src/*.h"]),
    deps = [":hdr_histogram_impl"],
    include_prefix = "src",
    visibility = ["//visibility:public"],
)

cc_library(
    name = "hdr_histogram_impl",
    srcs = glob([
        "src/*.h",
        "src/*.c",
    ]),
    deps = [
        "//zlib",
    ],
    copts = [
      "-Wall",
      "-Wno-unknown-pragmas",
      "-Wextra",
      "-Wshadow",
      "-Winit-self",
      "-Wmissing-prototypes",
      "-D_GNU_SOURCE",
      "-O3",
    ],
    linkstatic = 1,
    visibility = ["//visibility:private"],
)

cc_test(
  name = "perftest",
  srcs = [
    "test/hdr_histogram_perf.c",
  ],
  deps = [
    "//zlib",
    "//hdr_histogram",
  ],
)

cc_test(
name = "hdr_histogram_test",
srcs = [
"test/hdr_histogram_test.c",
],
deps = [
"//zlib",
"//hdr_histogram",
],
)

cc_test(
name = "hdr_histogram_log_test",
srcs = [
"test/hdr_histogram_log_test.c",
],
deps = [
"//zlib",
"//hdr_histogram",
],
)
