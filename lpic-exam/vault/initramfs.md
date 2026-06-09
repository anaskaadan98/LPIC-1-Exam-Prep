Initial RAM Filesystem is an archive containing a filesystem used as a temporary root filesystem during the boot process.

- The main job is to provide the required LKM so the kernel can access the real root filesystem of the operating system.
- Then the kernel will mount all filesystems configured in `/etc/fstab` and then will execute the first program, a utility named [[init utility|init]].
- Once the `init` program is loaded, the `initramfs` is removed from RAM.



```handwritten-ink
{
	"versionAtEmbed": "0.3.4",
	"filepath": "Ink/Writing/2026.6.8 - 17.28pm.writing"
}
```
