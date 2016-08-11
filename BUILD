cc_inc_library(
    name = "hdr_histogram",
    hdrs = glob(["src/*.h"]),
    deps = [":hdr_histogram_impl"],
    prefix = "src",
    visibility = ["//visibility:public"],
)

cc_library(
    name = "hdr_histogram_impl",
    srcs = glob([
        "src/*.h",
        "src/*.c",
    ]),
    linkstatic = 1,
    visibility = ["//visibility:private"],
)
