(ubuntu-26.10-release-notes)=
# Ubuntu 26.10 release notes

These release notes cover new features and changes in Ubuntu 26.10 (Stonking Stingray).

:::{important}
Ubuntu 26.10 (Stonking Stingray) is currently in development, scheduled to be released in October 2026.
:::

For the release schedule of Ubuntu 26.10, refer to the {ref}`release schedule <stonking-stingray-schedule>`.

:::{toctree}
:maxdepth: 1
:hidden:

Release schedule <schedule>
:::

## Support lifespan

## Upgrades


## New features and improvements

### Desktop features

### Server features

### Development features

#### Toolchain upgrades

| Toolchain | Version | Notes |
|-----------|---------|-------|
| GCC 🐄 | 15.2.0 | Includes latest patches for the GCC 15 series as well as support for C++ modules. [Release Notes](https://gcc.gnu.org/gcc-15/changes.html) |
| .NET 🦄 | 10.0.112 | Updated .NET runtimes with latest security fixes and toolchain capabilities. [Release Notes](https://github.com/dotnet/core/blob/main/release-notes/10.0/10.0.12/10.0.112.md) |
| Go 🐀 | 1.27 | Go 1.27 supports for generic methods and GODEBUG settings. [Release Notes](https://go.dev/doc/go1.27) |
| LLVM 🐉 | 22.1.6 | Includes targeted bug fixes and stability improvements with early support for C2y named loops and expanded SSE, AVX, AVX-512 intrinsics. [Release Notes](https://discourse.llvm.org/t/llvm-22-1-6-released/90838) |
| OpenJDK ☕ | 25.0.4 | OpenJDK release with many stability improvements and patches. [Release Notes](https://mail.openjdk.org/archives/list/jdk-updates-dev@openjdk.org/thread/BRREMPN6BLLC2CYAKLXGRHHNMCIQQSR5/) |
| Python 🐍 | 3.14.7 | Python 3.14.7 is the seventh maintenance release of 3.14, containing numerous bugfixes and improvements. [Release Notes](https://www.python.org/downloads/release/python-3147/) |
| Rust 🦀 | 1.97.1 | Rust 1.97 stable toolchain with LLVM miscompilation fixes. [Release Notes](https://blog.rust-lang.org/2026/07/16/Rust-1.97.1/) |
| Zig ⚡ | 0.16 | Zig is a general-purpose programming language and toolchain for maintaining robust, optimal, and reusable software. [Release Notes](https://ziglang.org/download/0.16.0/release-notes.html)|

### Enterprise features

### Cloud features

### Security features

#### An oxidized OpenPGP

Ubuntu 26.10 adopts the Rust-based Sequoia PGP into the main archive,
providing an officially supported, modern, and memory-safe OpenPGP
implementation.

The goal is for Sequoia PGP to become Ubuntu's default OpenPGP toolchain, with
`sq` and `sqv` serving as counterparts to the traditional `gpg` and `gpgv`
utilities, respectively. By adopting Sequoia, Ubuntu can maintain OpenPGP
interoperability while moving its core implementation toward a more
maintainable and memory-safe foundation.

:::{note}
`gpg` and `gpgv` are still available in the main repository as of Ubuntu 26.10.
:::

### Hardware support features

#### Support for new RISC-V platforms

Ubuntu 26.10 introduces official support for multiple RVA23 RISC-V platforms:
- The SpacemiT K3 boards (Pico-ITX, CoM260 kit)
- The SiFive BigSky platform

Documentation on how to install on the SpacemiT K3 boards is available: <https://ubuntu.com/hardware/docs/boards/how-to/ubuntu_supported/spacemit-k3/>.

Ubuntu Desktop and Xubuntu Minimal RISC-V desktop images are provided with support for the SpacemiT K3 and QEMU.

### System features

#### Linux kernel \<VERSION\>

#### systemd \<VERSION\>

#### 100% Rust `coreutils`

The default core utilities now run entirely on the Rust-based `uutils`
implementation. The remaining GNU utilities (`cp`, `mv`, and `rm`), previously
retained due to compatibility issues, have now been migrated.


## Backwards-incompatible changes

### Desktop changes

### Server changes

### Development changes

### Enterprise changes

### Cloud changes

### Security changes

#### OpenSSH split between two packages

OpenSSH in Ubuntu Server 26.10 has been split into two source packages: [`openssh`](https://launchpad.net/ubuntu/+source/openssh) and [`openssh-gssapi`](https://launchpad.net/ubuntu/+source/openssh-gssapi). The main difference between them is that [`openssh`](https://launchpad.net/ubuntu/+source/openssh) produces binary packages **without GSSAPI/Kerberos support**. That support has been moved to [`openssh-gssapi`](https://launchpad.net/ubuntu/+source/openssh-gssapi).

[`openssh-gssapi`](https://launchpad.net/ubuntu/+source/openssh-gssapi) produces:

 * `openssh-gssapi-server`: the server-side OpenSSH daemon with GSSAPI/Kerberos support.
 * `openssh-gssapi-client`: the client-side OpenSSH with GSSAPI

Whereas [openssh](https://launchpad.net/ubuntu/+source/openssh) produces:

 * `openssh-server`: the server-side OpenSSH daemon without GSSAPI/Kerberos support.
 * `openssh-client`: the client-side OpenSSH without GSSAPI/Kerberos support.
 * All the other regular `openssh` binary packages.

The `-gssapi` variants of these binary packages conflict with the non-`gssapi` ones. If one is installed, the other is removed.

This split was done to reduce the security exposure of the OpenSSH server and client binaries, as GSSAPI/Kerberos support is not required for many users. As explained in [#1141274](https://bugs.debian.org/cgi-bin/bugreport.cgi?bug=1141274), the GSSAPI/Kerberos support includes a sizeable patch that was never included by the upstream project, but is still very useful to users of such deployments, and relied upon. This package split allows users to install the OpenSSH server and client without GSSAPI/Kerberos support, while still allowing those who need it to install the GSSAPI/Kerberos-enabled versions.

On top of that, the Ubuntu packaging of [`openssh-gssapi`](https://launchpad.net/ubuntu/+source/openssh-gssapi) also includes the `ccache` patch (see [LP: #1889548](https://bugs.launchpad.net/ubuntu/+source/openssh-gssapi/+bug/1889548). This allows for forwarded credentials to be stored according to the `default_ccache_name` setting in `/etc/krb5.conf` on the target host, instead of forcing a randomly named file in `/tmp`.

The Ubuntu release upgrader tool (see [How to upgrade your Ubuntu release](https://ubuntu.com/server/docs/how-to/software/upgrade-your-release/)) will check the system being upgraded for indications that GSSAPI/Kerberos is being used with `openssh`, and automatically select `openssh-server-gssapi` or `openssh-client-gssapi` for installation, if appropriate. Fresh installs of Ubuntu 26.10, however, will default to the non-GSSAPI/Kerberos versions of the OpenSSH server and client binaries.

### Hardware support changes

### System changes


## Deprecated features

### Desktop deprecations

### Server deprecations

### Development deprecations

### Enterprise deprecations

### Cloud deprecations

### Security deprecations

### Hardware support deprecations

### System deprecations


## Bug fixes

### Desktop fixes

### Server fixes

### Development fixes

### Enterprise fixes

### Cloud fixes

### Security fixes

### Hardware support fixes

### System fixes


## Known issues

### Desktop issues

### Server issues

### Development issues

### Enterprise issues

### Cloud issues

### Security issues

### Hardware support issues

### System issues


## Official flavors

## More information
