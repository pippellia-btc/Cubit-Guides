# Cubit-Guides
The one-stop guide to getting Citadel up and running on your own Cubit.

This guide will cover how to install Citadel on two Cubit configurations:
1. OS on the NVMe drive, data on the RAID1 (server enthusiast edition and sovereign individual edition)
2. All on the NVMe drive (bitcoiner edition)

## Prerequisites

In order to use Cubit, you need SSH installed on your primary machine, being it a desktop or laptop. Linux and MacOS have it pre-installed; if you use Windows you will have to install it.

Here is a tutorial (Windows): https://youtu.be/g2I6en4Mdjo?feature=shared

## Step 1. Preliminaries

1.  Download ubuntu server 22.04 LTS from the official website here: https://ubuntu.com/download/server
2.  Flash it on your USB drive, using an App like Balena Etcher: https://etcher.balena.io/
3.  Remove the USB drive, plug it into Cubit, and power-on
4.  Repetetly press the `Del` key to enter the BIOS
5.  Use the arrow keys to go to the Boot tab and make sure the USB is the first option (highest priority)

_Extra: From the BIOS you can configure the speed of the fan (if it's PWM compatible)_

## Step 6. Installing Ubuntu Server

1. Proceed with the installation wizard, using the arrow keys to move and Enter
