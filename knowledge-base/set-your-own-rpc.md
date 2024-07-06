# Recommended hardware 

* 4core CPU
* 8GB RAM
* 30GB free disk space

# GUI Mode
## Download the installation package
Go to [https://github.com/aspectron/kaspa-ng/releases](https://github.com/aspectron/kaspa-ng/releases)

Download the latest corresponding binary installation file according to your operating system.

<img src="../images/download-kng.bmp">

## Run kaspa-ng

### Windows

Unzip the binary file, and enter the unzipped directory. Double-click the kaspa-ng.exe file to start the node.

### Macos-arm64

Unzip the binary file, and enter the unzipped directory. Double-click the kaspa-ng file to start the node.

<img src="../images/mac-sec-kng-1-en.png" width="45%">
<img src="../images/mac-sec-kng-2-en.png" width="45%">

Re-double-click the kaspa-ng file to start the node.

<img src="../images/mac-sec-kng-3-en.png">

### Linux distributions that support the deb application format

```bash
sudo dpkg -i ./kaspa-ng_0.2.6-pre-rc1_amd64.deb

kaspa-ng
```

## Graphic operation

<img src="../images/kng-1.png" width="30%">
<img src="../images/kng-2.png" width="30%">
<img src="../images/kng-3.png" width="30%">

## Data synchronization

Please wait for data synchronization to finish. The process is complete when the following message appears.

<img src="../images/kng-4.png">

# Command-line Mode

## Download the installation package
Go to [https://github.com/kaspanet/rusty-kaspa/releases](https://github.com/kaspanet/rusty-kaspa/releases)

Download the corresponding binary installation file according to your operating system.

<img src="../images/download-rusty-kaspa.png">

## Run rusty-kaspa node

Unzip the binary file, and enter the unzipped directory. Execute the following command on the console to start the node and keep the console window open to wait for the data synchronization to complete.

Note: For more command options, run kaspad --help. In particular, when --rpclisten-borsh=public, the rpc can be used by other devices. 

### Windows

```powershell
.\kaspad.exe --utxoindex --rpclisten-borsh=default --disable-upnp
```
### Macos-arm64

```bash
./kaspad --utxoindex --rpclisten-borsh=default --disable-upnp
```
The first time you run it, you need to make some security-related settings as shown below.

<img src="../images/mac-sec-rusty-1-en.png" width="45%">
<img src="../images/mac-sec-rusty-2-en.png" width="45%">

Re-execute the following command on the console.

<img src="../images/mac-sec-rusty-3-en.png">

### Linux

```bash
./kaspad --utxoindex --rpclisten-borsh=default --disable-upnp
```

## Data synchronization

Data synchronization takes approximately half an hour to one and a half hours, depending on your network and computer configuration. And when you see following messages, the synchronization is complete.

Note: Do not close the console window.

<img src="../images/sync-complete.png">

# Config kasware rpc

Follow the steps below to configure rpc to ws://127.0.0.1:17110.

<img src="../images/wallet-rpc-setting-1.png" width="30%">
<img src="../images/wallet-rpc-setting-2.png" width="30%">
<img src="../images/wallet-rpc-setting-3.png" width="30%">

