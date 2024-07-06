# Recommended hardware 

* 4core CPU
* 8GB RAM
* 30GB free disk space

# GUI Mode
## Download the installation package
Go to [https://github.com/aspectron/kaspa-ng/releases](https://github.com/aspectron/kaspa-ng/releases)

Download the latest corresponding binary installation file according to your operating system.

<img src="../images/download-kng.bmp" width="500">

## Run

### Windows

Unzip the binary file, and enter the unzipped directory. Double-click the kaspa-ng.exe file to start the node.

<img src="../images/kng-1.png" width="300">
<img src="../images/kng-2.png" width="300">
<img src="../images/kng-3.png" width="300">

Please wait for data synchronization to finish. The process is complete when the following message appears.

<img src="../images/kng-4.png" width="300">

### Macos

### Linux distributions that support the deb application format

```bash
sudo dpkg -i ./kaspa-ng_0.2.6-pre-rc1_amd64.deb

kaspa-ng
```
Graphic operation part is the same as windows.

# Command-line Mode

## Download the installation package
Go to [https://github.com/kaspanet/rusty-kaspa/releases](https://github.com/kaspanet/rusty-kaspa/releases)

Download the corresponding binary installation file according to your operating system.

<img src="../images/download-rusty-kaspa.png" width="500">

## Run rusty-kaspa node

Unzip the binary file, and enter the unzipped directory. Execute the following command on the console to start the node and keep the console window open to wait for the data synchronization to complete.

Note: For more command options, run kaspad --help. In particular, when --rpclisten-borsh=public, the rpc can be used by other devices. 

### windows

```powershell
.\kaspad.exe --utxoindex --rpclisten-borsh=default --disable-upnp
```
### macos

```bash
./kaspad --utxoindex --rpclisten-borsh=default --disable-upnp
```
The first time you run it, you need to make some security-related settings as shown below.

<img src="../images/macos-security-1-en.png" width="400">
<img src="../images/macos-security-2-en.png" width="500">

Re-execute the following command on the console.

<img src="../images/macos-security-3-en.png" width="400">

### linux

```bash
./kaspad --utxoindex --rpclisten-borsh=default --disable-upnp
```

## Data synchronization

Data synchronization takes approximately half an hour to one and a half hours, depending on your network and computer configuration. And when you see following messages, the synchronization is complete.

Note: Do not close the console window.

<img src="../images/sync-complete.png" width="500">

# Config kasware rpc

Follow the steps shown to configure rpc to ws://127.0.0.1:17110.

<img src="../images/wallet-rpc-setting-1.png" width="250">
<img src="../images/wallet-rpc-setting-2.png" width="250">
<img src="../images/wallet-rpc-setting-3.png" width="250">

