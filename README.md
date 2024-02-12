# Cubit-Guides
The one-stop guide to getting Citadel up and running on your own Cubit

----

This guide will cover **how to install Citadel** on two Cubit configurations:
1. **Recommended**: OS on the NVMe drive, data on the RAID1 (server enthusiast edition and sovereign individual edition)
2. All on the NVMe drive (bitcoiner edition)

## Step 0. Prerequisites

In order to use Cubit, you need **SSH installed** on your primary machine, being it a desktop or laptop. Linux and MacOS have it pre-installed; if you use Windows you will have to install it.
Here is a tutorial (Windows): https://youtu.be/g2I6en4Mdjo?feature=shared

## Step 1. Preliminaries

1.  Download `ubuntu server 22.04 LTS` from the official website here: https://ubuntu.com/download/server
2.  Flash it on your USB drive, using an App like **Balena Etcher**: https://etcher.balena.io/
3.  Safely remove the USB drive, plug it into Cubit, and power-on
4.  Repetetly press the `Del` key to enter the BIOS
5.  Use the arrow keys to go to the `Boot` tab and make sure the USB is the first option (highest priority)

_Extra: From the BIOS you can configure the speed of the fan (if it's PWM compatible)_

----

<details>
    <summary> <h2> Cubit RAID </h2> </summary>

## Step 2. Installing Ubuntu Server

1. Go through with the **installation wizard**. Select the default choice in all steps except those indicated below.
2. When you arrive at the storage configuration, select `Custom Storage`  and copy the following configuration you see in the image
![image](https://github.com/pippellia-btc/Cubit-Guides/assets/108896743/0e73deef-5af8-452d-9b99-9e68499cb40f)
3. Install OpenSSH


## Step 3. SSH into Cubit

1. After the installation, power up your Cubit and plug in the **ethernet cable**
2. Get the `ip_address` of your Cubit, using an App like Angry IP Scanner: https://angryip.org/
3. Open the **terminal** (or prompt in Windows), and SSH into your Cubit with the command `ssh [username]@ip_address`, using the `username` and `password` you specified during the installation
![image](https://github.com/pippellia-btc/Cubit-Guides/assets/108896743/5bc8fea7-b6e0-4d00-a91c-1a50b6208d51)


## Step 4. Installing Citadel
1. Configure the RAID: `sudo mdadm --create --verbose /dev/md0 --level=1 --raid-devices=2 /dev/sda /dev/sdb`
2. Install Docker: `curl -fsSL https://get.docker.com | sh`
3. Install Citadel dependencies: `sudo apt -y install fswatch jq rsync curl python3-requests python3-yaml git`
4. Download Citadel: `git clone https://gitlab.com/nirvati/citadel/lts/core.git ~/citadel`
5. Install Citadel: `sudo ~/citadel/scripts/citadel-os/cubit/install`
6. Create directories: `mkdir -p /home/cubit/citadel/app-data/bitcoin && mkdir -p /home/cubit/citadel/app-data/electrs`
7. Reboot: `sudo reboot`
8. Wait 5 min, then **SSH** again into Cubit
9. Test if the storage configuration works with `sudo systemctl status citadel-external-storage`
If it shows `active` everything should work. If you now run `lsblk` you should see something like this
![image](https://github.com/pippellia-btc/Cubit-Guides/assets/108896743/7e752172-f5de-4ee8-b8fb-4a44fca3fb13)

## Step 5. Start using Citadel
1.  Wait up to 10 min
2.  On any device that's connected to the home network, type Cubit's `ip_address` in a browser and start using Citadel!

_Note: The next time you reboot, your Ubuntu password will be the same as the password you entered on Citadel_

</details>


<details>
    <summary> <h2>Cubit single disk</h2></summary>

## Step 2. Installing Ubuntu Server

1. Go through with the **installation wizard**. Select the default choice in all steps except those indicated below.
2. When you arrive at the storage configuration, select `Custom Storage`  and copy the following configuration you see in the image
![3%](https://github.com/pippellia-btc/Cubit-Guides/assets/108896743/8dfa906b-924d-4cd5-852e-4aa134f99b16)
3. Install OpenSSH


## Step 3. SSH into Cubit

1. After the installation, power up your Cubit and plug in the **ethernet cable**
2. Get the `ip_address` of your Cubit, using an App like Angry IP Scanner: https://angryip.org/
3. Open the **terminal** (or prompt in Windows), and SSH into your Cubit with the command `ssh [username]@ip_address`, using the `username` and `password` you specified during the installation
![image](https://github.com/pippellia-btc/Cubit-Guides/assets/108896743/5bc8fea7-b6e0-4d00-a91c-1a50b6208d51)


## Step 4. Installing Citadel
1. Install Docker: `curl -fsSL https://get.docker.com | sh`
2. Install Citadel dependencies: `sudo apt -y install fswatch jq rsync curl python3-requests python3-yaml git`
3. Download Citadel: `git clone https://gitlab.com/nirvati/citadel/lts/core.git ~/citadel`
4. Install Citadel: `sudo ~/citadel/scripts/citadel-os/cubit/install`
5. Reboot: `sudo reboot`
6. Wait 5 min, then **SSH** again into Cubit
9. Test if configuration works with `sudo systemctl status citadel-startup`
If it shows `active` everything should work.

## Step 5. Start using Citadel
1.  Wait up to 10 min
2.  On any device that's connected to the home network, type Cubit's `ip_address` in a browser and start using Citadel!

_Note: The next time you reboot, your Ubuntu password will be the same as the password you entered on Citadel_

</details>
