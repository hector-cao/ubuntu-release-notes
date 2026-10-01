(ubuntu-26.10-release-notes)=
# Ubuntu 26.10 release notes

These release notes cover new features and changes in Ubuntu 26.10 (Stonking Stingray).

:::{important}
Ubuntu 26.10 (Stonking Stingray) is currently in development, scheduled to be released in October 2026.
:::

For the release schedule of Ubuntu 26.10, refer to:

:::{toctree}
:maxdepth: 1

Release schedule <schedule>
:::


## Support lifespan
## Upgrades
## New features in \<VERSION\>
### Updated Packages
### Linux kernel \<VERSION\> 🐧
### systemd \<VERSION\>
### Toolchain Upgrades 🛠️
### Default configuration changes ⚙️
### Ubuntu Desktop
### Ubuntu Foundations

#### 100% Rust coreutils

The default core utilities now run entirely on the Rust-based `uutils`
implementation. The remaining GNU utilities (`cp`, `mv`, and `rm`), previously
retained due to compatibility issues, have now been migrated.

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

### Ubuntu Server

#### openssh
OpenSSH in Ubuntu Server 26.10 has been split into two source packages: [openssh](https://launchpad.net/ubuntu/+source/openssh) and [openssh-gssapi](https://launchpad.net/ubuntu/+source/openssh-gssapi). The main difference between them is that [openssh](https://launchpad.net/ubuntu/+source/openssh) produces binary packages WITHOUT GSSAPI/Kerberos support. That support has been moved to [openssh-gssapi](https://launchpad.net/ubuntu/+source/openssh-gssapi).

[openssh-gssapi](https://launchpad.net/ubuntu/+source/openssh-gssapi) produces:
 * `openssh-gssapi-server` - the server-side OpenSSH daemon with GSSAPI/Kerberos support.
 * `openssh-gssapi-client` - the client-side OpenSSH with GSSAPI

Whereas [openssh](https://launchpad.net/ubuntu/+source/openssh) produces:
 * `openssh-server` - the server-side OpenSSH daemon without GSSAPI/Kerberos support.
 * `openssh-client` - the client-side OpenSSH without GSSAPI/Kerberos support.
 * and all the other regular openssh binary packages.

The `-gssapi` variants of these binary packages conflict with the non-gssapi ones. If one is installed, the other is removed.

This split was done to reduce the security exposure of the OpenSSH server and client binaries, as GSSAPI/Kerberos support is not required for many users. As explained in [#1141274](https://bugs.debian.org/cgi-bin/bugreport.cgi?bug=1141274), the GSSAPI/Kerberos support includes a sizeable patch that was never included by the upstream project, but is still very useful to users of such deployments, and relied upon. This package split allows users to install the OpenSSH server and client without GSSAPI/Kerberos support, while still allowing those who need it to install the GSSAPI/Kerberos-enabled versions.

On top of that, the Ubuntu packaging of [openssh-gssapi](https://launchpad.net/ubuntu/+source/openssh-gssapi) also includes the ccache patch (see [LP: #1889548](https://bugs.launchpad.net/ubuntu/+source/openssh-gssapi/+bug/1889548). This allows for forwarded credentials to be stored according to the `default_ccache_name` setting in `/etc/krb5.conf` on the target host, instead of forcing a randomly named file in `/tmp`.

The Ubuntu release upgrader tool (see [How to upgrade your Ubuntu release](https://ubuntu.com/server/docs/how-to/software/upgrade-your-release/)) will check the system being upgraded for indications that GSSAPI/Kerberos is being used with openssh, and automatically select `openssh-server-gssapi` and/or `openssh-client-gssapi` for installation, if appropriate. Fresh installs of Ubuntu 26.10, however, will default to the non-GSSAPI/Kerberos versions of the OpenSSH server and client binaries.

### OpenStack
### Platforms
## Known Issues
### General
### Linux kernel
### Ubuntu Desktop
### Ubuntu Server
## Official flavors
## More information
