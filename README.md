# buildkernel
A tool to build a secure-boot EFI stub kernel, and save it to the EFI system partition.

Originally written by sakaki to work with genkernel-next, a fork of genkernel.
genkernel-next was removed from the Gentoo repository in August 2020, and sakaki stood down as maintainer of buildkernel in October 2020 (see [here](https://github.com/sakaki-/buildkernel/issues/35)).
genkernel now has many of genkernel-next's features, excluding plymouth support, for which FlyingWaffle has written a [patch](https://bugs.gentoo.org/753617).
This is hijackeel's fork of buildkernel, made to work with genkernel 4.1.2 + FlyingWaffle's patch for Plymouth support.

## Description
**buildkernel** is a script that builds a Gentoo Linux EFI stub kernel which is suitable for booting from a USB key using UEFI (no additional bootloader required). It makes use of the initramfs creation tools (and early userspace **init**(8) script) provided by **genkernel**(8).

Specifically, the assumed use-case for buildkernel is where you are creating a kernel for use in a dual-factor-authenticated LVM-over-LUKS system, booting from an external USB key, with secure boot enabled (using UEFI), where you may (optionally) wish to use the **plymouth**(8) splash manager, and where the target (final) init system is **systemd**(1) or **OpenRC**(8).

**buildkernel** will automatically set the necessary kernel configuration parameters, including the command line, sign the resulting kernel if possible, then update the EFI boot list if required.

The **buildkernel** utility can be invoked in non-interactive (default) or interactive mode (see the **--ask** option, in the manpage). Non-interactive mode is suitable for use in a scripted invocation.

Certain key options can be specified via the configuration file, _/etc/buildkernel.conf_: see **buildkernel.conf**(5) for details.

Although **buildkernel** is targetted primarily at the use-case where the EFI system partition is on a removable USB key (for security), it can also be used with a system partition on a fixed drive.

## Installation

**buildkernel** is best installed (on Gentoo) via its ebuild, available as part of the **sakaki-tools-hjkl** [overlay](https://github.com/hijackeel/sakaki-tools-hjkl).
Full instructions are provided as part of the [**Sakaki's EFI Install Guide**](https://wiki.gentoo.org/wiki/Sakaki's_EFI_Install_Guide) tutorial, on the Gentoo wiki.

In particular, see [this section](https://wiki.gentoo.org/wiki/Sakaki's_EFI_Install_Guide/Configuring_and_Building_the_Kernel#What_the_buildkernel_Script_Does_.28Background_Reading.29) for a detailed description of what **buildkernel** does, and why.
