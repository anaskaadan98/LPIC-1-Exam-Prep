After the installation of the *Ubuntu* machine on *Virtual Box* you need to install the ***Virtualbox Guest Additions***.

`Devices -> Insert Guest Additions CD Image..`

On the Virtual machine run the command:

```bash
sudo apt update
sudo apt install build-essential dkms linux-headers-$(uname -r)
```

Go to CD directory and open terminal:

```bash
sudo ./VBoxLinuxAdditions.run
```

On the Guest machine run the following commands:

```bash
sudo apt update
sudo apt install virtualbox-guest-utils virtualbox-guest-x11
sudo reboot
```

If you messed up the installation you can remove old Guest Additions first:

```bash
sudo apt remove virtualbox-guest-utils virtualbox-guest-x11 virtualbox-guest-dkms
```

---