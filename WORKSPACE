workspace(name = "example")

load("@bazel_tools//tools/build_defs/repo:http.bzl", "http_file")
load("@bazel_tools//tools/build_defs/repo:http.bzl", "http_archive")

# Some file dependencies
http_file(
    name = "emacs",
    sha256 = "1439bf7f24e5769f35601dbf332e74dfc07634da6b1e9500af67188a92340a28",
    urls = [
        "https://storage.googleapis.com/engflow-tools-public/emacs-28.1.tar.gz",
        "https://mirror.its.dal.ca/gnu/emacs/emacs-28.1.tar.gz",
        "https://mirrors.kernel.org/gnu/emacs/emacs-28.1.tar.gz",
    ],
)

http_file(
    name = "ubuntu_20.04_1.3GB",
    sha256 = "5035be37a7e9abbdc09f0d257f3e33416c1a0fb322ba860d42d74aa75c3468d4",
    urls = [
        "https://storage.googleapis.com/engflow-tools-public/ubuntu-20.04.5-live-server-amd64.iso",
        "https://mirror.math.princeton.edu/pub/ubuntu-iso/focal/ubuntu-20.04.5-live-server-amd64.iso",
        "https://mirror.pit.teraswitch.com/ubuntu-releases/focal/ubuntu-20.04.5-live-server-amd64.iso",
    ],
)

http_archive(
    name = "rules_jvm_external",
    sha256 = "8c3b207722e5f97f1c83311582a6c11df99226e65e2471086e296561e57cc954",
    strip_prefix = "rules_jvm_external-5.1",
    url = "https://github.com/bazelbuild/rules_jvm_external/releases/download/5.1/rules_jvm_external-5.1.tar.gz",
)

http_archive(
    name = "com_google_googleapis",
    sha256 = "37285d1e8ca2d191f18575d9285de26fd1fd66204cb58a4df8371d7d72c5de22",
    strip_prefix = "googleapis-88a9a5f9944682d1901923cc1376935c2c694595",
    urls = [
        "https://github.com/googleapis/googleapis/archive/88a9a5f9944682d1901923cc1376935c2c694595.tar.gz",
    ],
)

http_archive(
    name = "com_engflow_engflowapis",
    sha256 = "f8f4b5aedc7a81b040680e7f1ed5d0f8cdc8b6ff3b8f32da213093f77fa0f52c",
    strip_prefix = "engflowapis-6554bb4d2732e2d4d6f667eb842e051442eaab08",
    urls = [
        "https://github.com/EngFlow/engflowapis/archive/6554bb4d2732e2d4d6f667eb842e051442eaab08.zip",
    ],
)

http_archive(
    name = "io_grpc_grpc_java",
    sha256 = "2afc5d3abb08bf15ed76cb7a99d06bddda16464955b91b1b65b73bd0a1113fa5",
    strip_prefix = "grpc-java-1.57.0",
    urls = [
        "https://github.com/grpc/grpc-java/archive/refs/tags/v1.57.0.zip",
    ],
)

http_archive(
    name = "io_bazel_rules_kotlin",
    sha256 = "fd92a98bd8a8f0e1cdcb490b93f5acef1f1727ed992571232d33de42395ca9b3",
    urls = [
        "https://github.com/bazelbuild/rules_kotlin/releases/download/v1.7.1/rules_kotlin_release.tgz",
    ],
)

http_archive(
    name = "io_bazel_rules_go",
    sha256 = "278b7ff5a826f3dc10f04feaf0b70d48b68748ccd512d7f98bf442077f043fe3",
    urls = [
        "https://github.com/bazelbuild/rules_go/releases/download/v0.41.0/rules_go-v0.41.0.zip",
    ],
)

http_archive(
    name = "rules_proto",
    sha256 = "66bfdf8782796239d3875d37e7de19b1d94301e8972b3cbd2446b332429b4df1",
    strip_prefix = "rules_proto-4.0.0",
    urls = [
        "https://github.com/bazelbuild/rules_proto/archive/refs/tags/4.0.0.tar.gz",
    ],
)

# Loads rules required to compile proto files
http_archive(
    name = "rules_proto_grpc",
    sha256 = "b244cbede34638ad0e1aec0769f62b8348c7ed71f431a027e252a07d6adba3d6",
    strip_prefix = "rules_proto_grpc-4.4.0",
    urls = [
        "https://github.com/rules-proto-grpc/rules_proto_grpc/archive/4.4.0.tar.gz",
    ],
)

load("@rules_proto_grpc//java:repositories.bzl", rules_proto_grpc_java_repos = "java_repos")

rules_proto_grpc_java_repos()

load("@rules_proto//proto:repositories.bzl", "rules_proto_dependencies", "rules_proto_toolchains")
load("@rules_jvm_external//:defs.bzl", "maven_install")

rules_proto_dependencies()

rules_proto_toolchains()

http_archive(
    name = "com_google_protobuf",
    sha256 = "ba639dbd4ae9992ef1ce52df6054ab49e98e800f9eeb0a5eb0fb9813058eb935",
    strip_prefix = "protobuf-21edc3b26fc80771baea78d8bd8df1285b12cae2",
    urls = [
        "https://github.com/protocolbuffers/protobuf/archive/21edc3b26fc80771baea78d8bd8df1285b12cae2.tar.gz",
    ],
)

load("@com_google_protobuf//:protobuf_deps.bzl", "protobuf_deps")

protobuf_deps()

load("@io_grpc_grpc_java//:repositories.bzl", "IO_GRPC_GRPC_JAVA_ARTIFACTS", "IO_GRPC_GRPC_JAVA_OVERRIDE_TARGETS", "grpc_java_repositories")

grpc_java_repositories()

load("@com_google_googleapis//:repository_rules.bzl", "switched_rules_by_language")

switched_rules_by_language(
    name = "com_google_googleapis_imports",
    java = True,
)

maven_install(
    artifacts = IO_GRPC_GRPC_JAVA_ARTIFACTS + [
        "commons-cli:commons-cli:1.5.0",
        "com.google.oauth-client:google-oauth-client:1.34.1",
    ],
    generate_compat_repositories = True,
    override_targets = IO_GRPC_GRPC_JAVA_OVERRIDE_TARGETS,
    repositories = [
        "https://repo.maven.apache.org/maven2/",
    ],
)

load("@maven//:compat.bzl", "compat_repositories")

compat_repositories()

http_archive(
    name = "io_bazel_rules_scala",
    sha256 = "d39aceb39808da3ee5d84f8d6e460be0568e946da71698fc1414fc696765200a",
    strip_prefix = "rules_scala-6.0.0",
    url = "https://github.com/bazelbuild/rules_scala/releases/download/v6.0.0/rules_scala-v6.0.0.tar.gz",
)

load("@io_bazel_rules_scala//:scala_config.bzl", "scala_config")

scala_config()

load("@io_bazel_rules_scala//scala:scala.bzl", "scala_repositories")

scala_repositories()

load("@io_bazel_rules_scala//scala:toolchains.bzl", "scala_register_toolchains")

scala_register_toolchains()

load("@io_bazel_rules_scala//testing:scalatest.bzl", "scalatest_repositories", "scalatest_toolchain")

scalatest_repositories()

scalatest_toolchain()

load("@io_bazel_rules_go//go:deps.bzl", "go_register_toolchains", "go_rules_dependencies")

go_rules_dependencies()

go_register_toolchains(version = "1.20.5")

load("@io_bazel_rules_kotlin//kotlin:repositories.bzl", "kotlin_repositories")

kotlin_repositories()

load("@io_bazel_rules_kotlin//kotlin:core.bzl", "kt_register_toolchains")

kt_register_toolchains()

http_archive(
    name = "aspect_rules_ts",
    sha256 = "4c3f34fff9f96ffc9c26635d8235a32a23a6797324486c7d23c1dfa477e8b451",
    strip_prefix = "rules_ts-1.4.5",
    urls = [
        "https://github.com/aspect-build/rules_ts/archive/refs/tags/v1.4.5.tar.gz",
    ],
)

load("@aspect_rules_ts//ts:repositories.bzl", "rules_ts_dependencies")

rules_ts_dependencies(ts_version_from = "//typescript:package.json")

load("@rules_nodejs//nodejs:repositories.bzl", "DEFAULT_NODE_VERSION", "nodejs_register_toolchains")

nodejs_register_toolchains(
    name = "node",
    node_version = DEFAULT_NODE_VERSION,
)

load("@aspect_bazel_lib//lib:repositories.bzl", "register_copy_directory_toolchains", "register_copy_to_directory_toolchains")

register_copy_directory_toolchains()

register_copy_to_directory_toolchains()

load("@bazel_skylib//:workspace.bzl", "bazel_skylib_workspace")

bazel_skylib_workspace()

http_archive(
    name = "io_bazel_rules_dotnet",
    sha256 = "5098268d2950d658a0ab5558fa9faa590866be7ff1b20a97964b37720f8af2c6",
    strip_prefix = "rules_dotnet-0b7ae93fa81b7327a655118da0581db5ebbe0b8d",
    urls = [
        "https://github.com/bazelbuild/rules_dotnet/archive/0b7ae93fa81b7327a655118da0581db5ebbe0b8d.zip",
    ],
)

load("@io_bazel_rules_dotnet//dotnet:deps.bzl", "dotnet_repositories")

dotnet_repositories()

load("@io_bazel_rules_dotnet//dotnet:defs.bzl", "dotnet_register_toolchains", "dotnet_repositories_nugets")

dotnet_register_toolchains()

dotnet_repositories_nugets()

http_archive(
    name = "rules_perl",
    sha256 = "d8ca5b2aacf91e1eacc3c6b90e833efa8537ece7c746aa9ccfbab1fc354abbb4",
    strip_prefix = "rules_perl-d458b41dd15a086721dcf663317f2c121bba8984",
    urls = [
        "https://github.com/bazelbuild/rules_perl/archive/d458b41dd15a086721dcf663317f2c121bba8984.zip",
    ],
)

load("@rules_perl//perl:deps.bzl", "perl_register_toolchains", "perl_rules_dependencies")

perl_rules_dependencies()

perl_register_toolchains()

http_archive(
    name = "rules_python",
    sha256 = "0a8003b044294d7840ac7d9d73eef05d6ceb682d7516781a4ec62eeb34702578",
    strip_prefix = "rules_python-0.24.0",
    url = "https://github.com/bazelbuild/rules_python/archive/refs/tags/0.24.0.tar.gz",
)

load("@rules_python//python:pip.bzl", "pip_parse")

pip_parse(
    name = "pip_deps",
    requirements_lock = "//python:requirements_lock.txt",
)

load("@pip_deps//:requirements.bzl", "install_deps")

install_deps()

# Abseil Python can be imported through pip_import, but it has native Bazel support too.
http_archive(
    name = "io_abseil_py",
    sha256 = "0fb3a4916a157eb48124ef309231cecdfdd96ff54adf1660b39c0d4a9790a2c0",
    strip_prefix = "abseil-py-1.4.0",
    url = "https://github.com/abseil/abseil-py/archive/refs/tags/v1.4.0.tar.gz",
)

http_archive(
    name = "build_bazel_rules_swift",
    sha256 = "bf2861de6bf75115288468f340b0c4609cc99cc1ccc7668f0f71adfd853eedb3",
    url = "https://github.com/bazelbuild/rules_swift/releases/download/1.7.1/rules_swift.1.7.1.tar.gz",
)

load(
    "@build_bazel_rules_swift//swift:repositories.bzl",
    "swift_rules_dependencies",
)

swift_rules_dependencies()

load(
    "@build_bazel_rules_swift//swift:extras.bzl",
    "swift_rules_extra_dependencies",
)

swift_rules_extra_dependencies()
