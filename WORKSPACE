workspace(name = "Torch-TensorRT")

load("@bazel_tools//tools/build_defs/repo:http.bzl", "http_archive")
load("@bazel_tools//tools/build_defs/repo:git.bzl", "git_repository")

http_archive(
    name = "rules_python",
    sha256 = "778197e26c5fbeb07ac2a2c5ae405b30f6cb7ad1f5510ea6fdac03bded96cc6f",
    url = "https://github.com/bazelbuild/rules_python/releases/download/0.2.0/rules_python-0.2.0.tar.gz",
)

load("@rules_python//python:pip.bzl", "pip_install")

http_archive(
    name = "rules_pkg",
    sha256 = "038f1caa773a7e35b3663865ffb003169c6a71dc995e39bf4815792f385d837d",
    urls = [
        "https://mirror.bazel.build/github.com/bazelbuild/rules_pkg/releases/download/0.4.0/rules_pkg-0.4.0.tar.gz",
        "https://github.com/bazelbuild/rules_pkg/releases/download/0.4.0/rules_pkg-0.4.0.tar.gz",
    ],
)

load("@rules_pkg//:deps.bzl", "rules_pkg_dependencies")

rules_pkg_dependencies()

git_repository(
    name = "googletest",
    commit = "703bd9caab50b139428cea1aaff9974ebee5742e",
    remote = "https://github.com/google/googletest",
    shallow_since = "1570114335 -0400",
)

# External dependency for torch_tensorrt if you already have precompiled binaries.
# local_repository(
#     name = "torch_tensorrt",
#     path = "/opt/conda/lib/python3.8/site-packages/torch_tensorrt"
# )

# CUDA should be installed on the system locally
new_local_repository(
    name = "cuda",
    build_file = "@//third_party/cuda:BUILD",
    path = "/usr/local/cuda-11.4/",
)

new_local_repository(
    name = "cublas",
    build_file = "@//third_party/cublas:BUILD",
    path = "/usr",
)
#############################################################################################################
# Tarballs and fetched dependencies (default - use in cases when building from precompiled bin and tarballs)
#############################################################################################################

# http_archive(
#     name = "libtorch",
#     build_file = "@//third_party/libtorch:BUILD",
#     sha256 = "8d9e829ce9478db4f35bdb7943308cf02e8a2f58cf9bb10f742462c1d57bf287",
#     strip_prefix = "libtorch",
#     urls = ["https://download.pytorch.org/libtorch/cu113/libtorch-cxx11-abi-shared-with-deps-1.11.0%2Bcu113.zip"],
# )

# http_archive(
#     name = "libtorch_pre_cxx11_abi",
#     build_file = "@//third_party/libtorch:BUILD",
#     sha256 = "90159ecce3ff451f3ef3f657493b6c7c96759c3b74bbd70c1695f2ea2f81e1ad",
#     strip_prefix = "libtorch",
#     urls = ["https://download.pytorch.org/libtorch/cu113/libtorch-shared-with-deps-1.11.0%2Bcu113.zip"],
# )

# Download these tarballs manually from the NVIDIA website
# Either place them in the distdir directory in third_party and use the --distdir flag
# or modify the urls to "file:///<PATH TO TARBALL>/<TARBALL NAME>.tar.gz

# http_archive(
#     name = "cudnn",
#     build_file = "@//third_party/cudnn/archive:BUILD",
#     sha256 = "5500953c08c5e5d1dddcfda234f9efbddcdbe43a53b26dc0a82c723fa170c457",
#     strip_prefix = "cudnn-linux-x86_64-8.3.2.44_cuda11.5-archive",
#     urls = [
#         "https://developer.nvidia.com/compute/cudnn/secure/8.3.2/local_installers/11.5/cudnn-linux-x86_64-8.3.2.44_cuda11.5-archive.tar.xz",
#     ],
# )

# http_archive(
#     name = "tensorrt",
#     build_file = "@//third_party/tensorrt/archive:BUILD",
#     sha256 = "0cd8071d717f1b870ada79ce5889ab3d702439c356e96cbef23d0b469007fcb4",
#     strip_prefix = "TensorRT-8.4.0.6",
#     urls = [
#         "https://developer.nvidia.com/compute/machine-learning/tensorrt/secure/8.4.0/tars/tensorrt-8.4.0.6.linux.x86_64-gnu.cuda-11.6.cudnn8.3.tar.gz",
#     ],
# )

####################################################################################
# Locally installed dependencies (use in cases of custom dependencies or aarch64)
####################################################################################

# NOTE: In the case you are using just the pre-cxx11-abi path or just the cxx11 abi path
# with your local libtorch, just point deps at the same path to satisfy bazel.

# NOTE: NVIDIA's aarch64 PyTorch (python) wheel file uses the CXX11 ABI unlike PyTorch's standard
# x86_64 python distribution. If using NVIDIA's version just point to the root of the package
# for both versions here and do not use --config=pre-cxx11-abi

new_local_repository(
   name = "libtorch",
   path = "/usr/local/lib/python3.8/dist-packages/torch",
   build_file = "third_party/libtorch/BUILD"
)

new_local_repository(
   name = "libtorch_pre_cxx11_abi",
   path = "/usr/local/lib/python3.8/dist-packages/torch",
   build_file = "third_party/libtorch/BUILD"
)

new_local_repository(
   name = "cudnn",
   path = "/usr/",
   build_file = "@//third_party/cudnn/local:BUILD"
)

new_local_repository(
  name = "tensorrt",
  path = "/usr/",
  build_file = "@//third_party/tensorrt/local:BUILD"
)

# #########################################################################
# # Testing Dependencies (optional - comment out on aarch64)
# #########################################################################
# pip_install(
#     name = "torch_tensorrt_py_deps",
#     requirements = "//py:requirements.txt",
# )

# pip_install(
#     name = "py_test_deps",
#     requirements = "//tests/py:requirements.txt",
# )

pip_install(
    name = "pylinter_deps",
    requirements = "//tools/linter:requirements.txt",
)
