---
Weight: "1"
---
# Types of Hybervisors on Linux

1. **KVM (Kernel-based Virtual Machine)**
	KVM is built directly into the Linux kernel and turns Linux into hypervisor. It is usually used together with QEMU.
2. **Xen**
	One of the earliest enterprise-grade hypervisors
3. **QEMU**
	QMEU is technically emulator and virtualizer.
4. **VirtualBox**
	Popular for desktop users
5. **Proxmox VE**
	Technically not a hypervisor itself.

# Types of Virtual Machines
## Full Virtualization

The hypervisor completely emulates the underlying hardware, allowing guest operating systems to run unmodified.

**Advantages**:
- Runs unmodified operating systems
- Excellent compatibility
- Easy migration of existing systems

**Disadvantages**:
- More overhead from hardware emulation
- Potentially lower performance
## Paravirtualization

The guest OS is modified to be aware of the hypervisor and communicates directly with it.

**Advantages**:
- Better CPU and I/O performance
- Lower virtualization overhead

**Disadvantages**:
- Requires OS modifications
- Cannot run proprietary operating systems unless they support paravirtualization
## Hybrid Virtualization

Combines full virtualization with paravirtualized drivers or optimization to improve performance.

**Advantages**:
- High compatibility
- Near-native performance
- No need to modify the guest OS kernel

**Disadvantages**:
- Requires installation of optimized guest drivers for best performance.

# Working with Virtual Machine Templates

It is easy to create *templates* that can be customized for particular deployment scenarios. Often a virtual machine will have a basic operating system installation and some pre-configured authentication configuration settings set up to ease future system launches. This cuts down on the amount of time it takes to build a new system by reducing the amount of work that is often repeated, such as base package installation and locale settings.

This virtual machine template could then later get copied to a new guest system. In this case, the new guest would get renamed, a new MAC address generated for its network interface, and other modifications can be made depending on its intended use.

## The D-Bus Machine ID

Many Linux installation will utilize a machine identification number generated at install time, called the *D-Bus machine ID*. However, if a virtual machine is *cloned* to be used as a template for other virtual machine installations, a new D-Bus machine Id would need to be created to ensure the system resources from the hypervisor get directed to the appropriate guest system.


# Deploying Virtual Machines to the Cloud

Cloud **IaaS (Infrastructure as a Service)**  providers use hypervisors to host virtual machines and offer tools for creating, deploying, configuring, and migrating Linux-based VM images.

When deploying Linux system in a cloud environment, administrators should focus on three key areas:

1. Computing Instances
	- Costs are often based on CPU usage and the number of virtual machines running.
	- Proper capacity planning helps avoid unnecessary expenses
	- More VM instances generally result in higher charges
2. Block Storage
	- Cloud providers offer different types of storage for files and virtual machines
	- Pricing depends on storage capacity and performance
	- High-speed storage is more expensive, while archival ("data at rest") storage is typically cheaper.
3. Networking
	- Providers supply tools for configuring virtual networks, subnets, routing, firewalls, and DNS
	- Public DNS names can be assigned to internet-facing systems
	- Hybrid cloud solutions can connect on-premises infrastructure to cloud environments using VPNs


## Securely Accessing Guests in the Cloud

The most prevalent method in use for accessing a remote virtual guest on a cloud platform is through the use of OpenSSH software. A Linux system that resides in the cloud would have the OpenSSH server running, while an administrator would use an OpenSSH client with pre-shared keys for remote access.

## Preconfiguring Cloud Systems

**cloud-init** is a vendor-independent tool that automates the deployment and initial configuration of Linux virtual machines across many cloud (IaaS) providers

Key features:
- Uses **YAML** configuration files to define system settings.
- Can automatically configure:
	- Network settings
	- Software packages
	- SSH keys
	- User accounts
	- Locale and regional settings
	- Other system options
- Runs during a VM's **first boot** and applies the prdefined configuration.
- Simplifies the rapid depoyment of multiple cloud-based Linux systems with consistent settings.

# Containers

Provides isolated environments for running applications, similar to virtual machines, but with much less overhead because they do not emulate an entire computer or operating system.

Key points:
- Containers are lightweight and use only the resources needed to run an application
- They offer greater flexibility than virtual machines in some scenarios
- Containers can be migrated between hosts while the application continues running, whereas virtual machines may require shutdown before migration
- Multiple application version can run simultaneously, making updates and deployments easier
- Old containers can be automatically removed as uses finish their session

**cgroups (Control Groups)**

Containers rely on the Linux kernel's **cgroups** feature, which allows administrators to control and allocate system resources such as:
- CPU time
- Memory
- Disk bandwidth
- Network bandwidth
Container software uses cgroups to:
- Isolate applications
- Limit resource usage
- Simplify deployment and management

---