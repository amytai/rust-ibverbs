# ibverbs

[![Crates.io](https://img.shields.io/crates/v/ibverbs.svg)](https://crates.io/crates/ibverbs)
[![Documentation](https://docs.rs/ibverbs/badge.svg)](https://docs.rs/ibverbs/)
[![Build Status](https://travis-ci.org/jonhoo/rust-ibverbs.svg?branch=master)](https://travis-ci.org/jonhoo/rust-ibverbs)

Rust API wrapping the `ibverbs` RDMA library.

`libibverbs` is a library that allows userspace processes to use RDMA "verbs" to perform
high-throughput, low-latency network operations.

A good place to start is to look at the programs in [`examples/`](examples/), and the upstream
[C examples]. You can test RDMA programs on modern Linux kernels even without specialized RDMA
hardware by using [SoftRoCE][soft].

For more information on RDMA verbs, see the [InfiniBand Architecture Specification][infini]
vol. 1, especially chapter 11, and the RDMA Consortium's [RDMA Protocol Verbs
Specification][RFC5040]. See also the upstream [`libibverbs/verbs.h`] file for the original C
definitions, as well as the manpages for the `ibv_*` methods.

## Library dependency

`libibverbs` is usually available as a free-standing [library package]. It [used to be][1]
self-contained, but has recently been adopted into [`rdma-core`]. `cargo` will automatically
build the necessary library files and place them in `vendor/rdma-core/build/lib`. If a
system-wide installation is not available, those library files can be used instead by copying
them to `/usr/lib`, or by adding that path to the dynamic linking search path.

## Hardware support

iWARP ethernet NICs support RDMA over hardware-offloaded TCP/IP, while InfiniBand is a general
high-throughput, low-latency networking technology. InfiniBand host channel adapters (HCAs) and
iWARP NICs commonly support direct hardware access from userspace (kernel bypass), and
libibverbs supports this when available.

## Thread safety

All interfaces are `Sync` and `Send` since the underlying ibverbs API [is thread safe][safe].

[`rdma-core`]: https://github.com/linux-rdma/rdma-core
[`libibverbs/verbs.h`]: https://github.com/linux-rdma/rdma-core/blob/master/libibverbs/verbs.h
[library package]: https://launchpad.net/ubuntu/+source/libibverbs
[C examples]: https://github.com/linux-rdma/rdma-core/tree/master/libibverbs/examples
[1]: https://git.kernel.org/pub/scm/libs/infiniband/libibverbs.git/about/
[infini]: http://www.infinibandta.org/content/pages.php?pg=technology_public_specification
[RFC5040]: https://tools.ietf.org/html/rfc5040
[safe]: http://www.rdmamojo.com/2013/07/26/libibverbs-thread-safe-level/
[soft]: https://github.com/SoftRoCE/rxe-dev/wiki/rxe-dev:-Home