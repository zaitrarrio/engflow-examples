name: CI

on:
  push:
    branches:
      - "main"
  pull_request:
    branches:
      - "main"

# Recommended here: https://github.com/bazelbuild/bazelisk/issues/88#issuecomment-625178467
env:
  BAZELISK_GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
  GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}

jobs:
  test-matrix:
    runs-on: ${{ matrix.os }}
    strategy:
      fail-fast: false
      matrix:
        os: [ubuntu-latest, macos-latest, windows-latest]
    steps:
      - uses: actions/checkout@v3

      - name: Building //cpp directory
        run: bazel build //cpp/...

      - name: Building //docker directory
        run: bazel build //docker/...

      - name: Building //genrules directory
        run: bazel build //genrules/...

      - name: Building //go directory
        run: bazel build //go/...

      - name: Testing //java/com/engflow/example directory
        run: |
          bazel test //java/com/engflow/example/...

      - name: Building //kotlin directory
        run: bazel build //kotlin/...

      - name: Testing //scala directory
        run: |
          bazel test //scala/...

      - name: Testing //typescript directory
        run: |
          bazel test //typescript/...

      - name: Building //csharp directory
        run: bazel build //csharp/...

      - name: Building //perl directory
        run: bazel build //perl/...

      - name: Testing //python directory
        run: |
          bazel run //python:requirements.update
          bazel test //python/...

      - uses: swift-actions/setup-swift@v1
        if: matrix.os == 'ubuntu-latest'

      - name: Testing //swift directory
        run: bazel test --config=clang //swift:tests
