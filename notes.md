# Unix System Admin Handbook Notes

## Chapter 1

#### man
This command searches for the man pages after being given a keyword. For example
<pre>
man -k <i>keyword</i>
</pre>
Man pages are stored in the directory **/usr/share/man**. Cached versions of man are stored in **/var/cache/man**

The default search path for **man** could be known by entering the following command

<pre>
man
</pre>

The search path could be altered by overriding the env variable as following
<pre>
export MANPATH=/home/share/localman:/usr/share/man
</pre>

### Determining whether some package is installed or not
We can determine if a binary is in our search path by using following command
<pre>
which <i>binary</i>
</pre>

If which can't find it, try whereis
<pre>
whereis <i>binary</i>
</pre>

Another alternative is **locate** which uses a compiled index to seacch for filenames using a given pattern
<pre>
locate <i>file</i>
</pre>

### Installing a package from source 
<pre>
cd /tmp

## Unzip or clone project_directory here

cd <i>project_directory</i>

./configure

make

sudo make install
</pre>

Using **--prefix=*directory*** we can specify the installation directory other than the default which is **/usr/local** 

## Chapter 2

The boot process consists of a few broadly defined tasks:
* Finding, loading, and running bootstrapping code
* Finding, loading, and running the OS kernel
* Running startup scripts and system daemons
* Maintaining process hygiene and managing system state transitions

Linus distros now use system manager daemon called systemd instead of using init.systemd

### System Firmware

Firmware knows all the devices that live on the motherboard.

The firmware UI lets designate boot device usually by priotising a list of available options (e.g. Hard drive, USB etc.)

#### BIOS vs UEFI
Tradiotionally the firmware was caled BIOS (Basic Input Output System).

Modern standard is UEFI (Unified Extensible Firmware Interface)

#### Legacy BIOS
Traditional BIOS assumes that the boot device starts with a record called the MBR
(Master Boot Record). The MBR includes both a first-stage boot loader (aka “boot
block”) and a primitive disk partitioning table.

In one typical scenario, the boot block reads the partitioning information
from the MBR and identifies the disk partition marked as “active.” It then reads and
executes the second-stage boot loader from the beginning of that partition. This
scheme is known as a volume boot record.

You can see the boot configuration on a unix system using the command
<pre>
efibootmgr -v
</pre>

Modify the bootconfig using
<pre>
sudo efibootmgr -o <i>boot_option</i>
</pre>

#### Boot Loaders
The boot loader’s main job is to identify and load an appropriate operating system
kernel. Most boot loaders can also present a boot-time user interface that lets you
select which of several possible kernels or operating systems to invoke.


#### GRUB : Grand Unifed Boot Loader

This is the default boot loader in most Linux systems.

Grub cofig is kept in the **grub.cfg** file in **/boot/grub** or **/boot/grub2** depending on which Linux distro it is.

You can view grub config using
<pre>
cat /boot/grub/grub.cfg

## Alternatively

cat /boot/grub2/grub.cfg
</pre>

You can update the **grub.cfg** file to modify the grub configuration.

Alternatively you can run **grub-mkconfig** or **update-grub** (Debian and Ubuntu) to update grub config. 

Update the sh variables in **/etc/default/grub** and run the above commands to update the config.
