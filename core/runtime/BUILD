package(default_visibility = ["//visibility:public"])

config_setting(
    name = "use_pre_cxx11_abi",
    values = {
        "define": "abi=pre_cxx11_abi",
    },
)

cc_library(
    name = "runtime",
    srcs = [
        "CudaDevice.cpp",
        "DeviceList.cpp",
        "execute_engine.cpp",
        "TRTEngine.cpp",
        "register_jit_hooks.cpp",
        "runtime.cpp"
    ],
    hdrs = [
        "runtime.h",
    ],
    deps = [
        "@tensorrt//:nvinfer",
        "//core/util:prelude",
        "//core/plugins:torch_tensorrt_plugins"
    ] + select({
        ":use_pre_cxx11_abi": ["@libtorch_pre_cxx11_abi//:libtorch"],
        "//conditions:default": ["@libtorch//:libtorch"],
    }),
    alwayslink = True,
)

load("@rules_pkg//:pkg.bzl", "pkg_tar")

pkg_tar(
    name = "include",
    srcs = ["runtime.h"],
    package_dir = "core/runtime/",
)
