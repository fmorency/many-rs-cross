# `many-rs` cross-compilation attempt

Based on `many-rs` revision `472712f9b9553c5beb53c5e3c1d758f07a4a182b`

```shell
$ bazel build --platforms=//:linux-aarch64 --extra_toolchains=@llvm_toolchain_with_sysroot//:cc-toolchain-aarch64-linux //...
```

Fails to link with

```shell
 = note: ld.lld: error: undefined symbol: fstat64
          >>> referenced by fs.rs:1009 (library/std/src/sys/unix/fs.rs:1009)
          >>>               std-5e17e5117b93a26c.std.bc4647e0-cgu.0.rcgu.o:(std::fs::buffer_capacity_required::h87a0125b04f49ca2) in archive /home/fmorency/.cache/bazel/_bazel_fmorency/1b9b0f09909ec2a9cffa7ce4feab1a7a/external/rust-linux-aarch64__aarch64-unknown-linux-gnu__nightly_tools/lib/rustlib/aarch64-unknown-linux-gnu/lib/libstd-5e17e5117b93a26c.rlib
          >>> referenced by fs.rs:1009 (library/std/src/sys/unix/fs.rs:1009)
          >>>               std-5e17e5117b93a26c.std.bc4647e0-cgu.0.rcgu.o:(std::backtrace_rs::symbolize::gimli::mmap::hb24f5017b37ff140) in archive /home/fmorency/.cache/bazel/_bazel_fmorency/1b9b0f09909ec2a9cffa7ce4feab1a7a/external/rust-linux-aarch64__aarch64-unknown-linux-gnu__nightly_tools/lib/rustlib/aarch64-unknown-linux-gnu/lib/libstd-5e17e5117b93a26c.rlib
          >>> did you mean: fstat64@GLIBC_2.33
          >>> defined in: external/org_ll_sysroot_linux_aarch64/lib/aarch64-linux-gnu/libc.so.6
          
          ld.lld: error: undefined symbol: stat64
          >>> referenced by fs.rs:1482 (library/std/src/sys/unix/fs.rs:1482)
          >>>               std-5e17e5117b93a26c.std.bc4647e0-cgu.0.rcgu.o:(std::sys::common::small_c_string::run_with_cstr_allocating::h56d025d60e5c6ba9) in archive /home/fmorency/.cache/bazel/_bazel_fmorency/1b9b0f09909ec2a9cffa7ce4feab1a7a/external/rust-linux-aarch64__aarch64-unknown-linux-gnu__nightly_tools/lib/rustlib/aarch64-unknown-linux-gnu/lib/libstd-5e17e5117b93a26c.rlib
          >>> referenced by fs.rs:1482 (library/std/src/sys/unix/fs.rs:1482)
          >>>               std-5e17e5117b93a26c.std.bc4647e0-cgu.0.rcgu.o:(std::sys::unix::fs::stat::h2b943d7f1c11da2f) in archive /home/fmorency/.cache/bazel/_bazel_fmorency/1b9b0f09909ec2a9cffa7ce4feab1a7a/external/rust-linux-aarch64__aarch64-unknown-linux-gnu__nightly_tools/lib/rustlib/aarch64-unknown-linux-gnu/lib/libstd-5e17e5117b93a26c.rlib
          >>> did you mean: stat64@GLIBC_2.33
          >>> defined in: external/org_ll_sysroot_linux_aarch64/lib/aarch64-linux-gnu/libc.so.6
          clang: error: linker command failed with exit code 1 (use -v to see invocation)
```

More notes at https://github.com/liftedinit/many-rs/issues/313#issuecomment-1477958851